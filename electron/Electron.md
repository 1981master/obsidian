deffufa-frontend/                     ← project root
├─ deffufa-ui/                        ← React app source
│   ├─ src/
│   ├─ public/
│   └─ package.json
├─ electron/                           ← Electron app
│   ├─ main.js                         ← updated for new build path
│   ├─ preload.js
│   ├─ backend/                        ← backend JAR + JRE
│   ├─ assets/
│   └─ package.json                    ← updated scripts & build config
├─ build/                              ← React production build (auto-generated)
└─ dist/                               ← Electron-builder output

```json
{
  "name": "deffufa-ui",
  "version": "0.1.0",
  "description": "Deffufa desktop application",
  "author": "Mohammed",
  "private": true,
  "main": "main.js",
  "dependencies": {
    "axios": "^1.13.5",
    "react": "18.2.0",
    "react-dom": "18.2.0",
    "react-redux": "^9.2.0",
    "react-router-dom": "^7.14.0"
  },
  "devDependencies": {
    "electron": "^25.0.0",
    "electron-builder": "^26.8.1",
    "wait-on": "^7.0.1",
    "typescript": "^4.9.5",
    "cpx": "^1.5.0"
  },
  "scripts": {
    "build-react": "yarn --cwd ../deffufa-ui install && yarn --cwd ../deffufa-ui build && cpx \"../deffufa-ui/build/**/*\" ../build",
    "electron": "electron .",
    "dist": "npm run build-react && electron-builder"
  },
  "build": {
    "appId": "com.deffufa.app",
    "productName": "Deffufa",
    "directories": {
      "buildResources": "assets",
      "output": "dist"
    },
    "files": [
      "main.js",
      "preload.js",
      "build/**/*",
      "assets/**/*",
      "backend/**/*"
    ],
    "extraResources": [
      {
        "from": "backend/",
        "to": "backend",
        "filter": ["**/*"]
      }
    ],
    "win": {
      "icon": "assets/dvs.ico",
      "target": ["nsis"]
    },
    "nsis": {
      "oneClick": false,
      "allowToChangeInstallationDirectory": true,
      "createDesktopShortcut": true,
      "createStartMenuShortcut": true,
      "shortcutName": "Deffufa"
    },
    "mac": {
      "icon": "assets/dvs.icns"
    },
    "asarUnpack": [
      "backend/deffufa-0.0.1-SNAPSHOT.jar",
      "backend/jre/**",
      "backend/**",
      "build/**"
    ]
  }
}
```

---
```javascript

const path = require('path');
const { app, BrowserWindow, dialog, session } = require('electron');
const fs = require('fs');
const os = require('os');
const { spawn, execSync } = require('child_process');
const http = require('http');

let mainWindow, backendProcess;

const BACKEND_PORT = 8080;
const USE_H2 = true;
const dbFolder = path.join(os.homedir(), 'DeffufaData');
const isDev = !app.isPackaged;

// Backend paths
const backendJar = isDev
  ? path.join(__dirname, 'backend', 'deffufa-0.0.1-SNAPSHOT.jar')
  : path.join(process.resourcesPath, 'backend', 'deffufa-0.0.1-SNAPSHOT.jar');

const javaPath = isDev
  ? path.join(__dirname, 'backend', 'jre', 'bin', process.platform === 'win32' ? 'java.exe' : 'java')
  : path.join(process.resourcesPath, 'backend', 'jre', 'bin', process.platform === 'win32' ? 'java.exe' : 'java');

// Logging
const logFile = path.join(os.homedir(), 'deffufa-backend.log');
function log(msg) { fs.appendFileSync(logFile, `[${new Date().toISOString()}] ${msg}\n`); }

// Kill orphan H2
function killOrphanH2() { /* ... same as before ... */ }

// Cleanup backend
function cleanupBackend() { if (backendProcess && !backendProcess.killed) backendProcess.kill('SIGTERM'); }

// Wait for backend ready
function waitForBackendReady(port, callback, retries = 30, intervalMs = 1000) {
  let attempts = 0;
  const check = () => {
    const req = http.request({ method: 'GET', hostname: 'localhost', port, path: '/' }, (res) => {
      log(`Backend ready (status ${res.statusCode})`);
      callback();
    });
    req.on('error', () => {
      if (++attempts < retries) setTimeout(check, intervalMs);
      else { dialog.showErrorBox('Error', `Backend failed to start. Check log: ${logFile}`); app.quit(); }
    });
    req.end();
  };
  check();
}

// Start backend
function startBackend(jarPath, dbFolder, callback) {
  if (!fs.existsSync(dbFolder)) fs.mkdirSync(dbFolder, { recursive: true });
  killOrphanH2();
  const jdbcUrl = USE_H2
    ? `jdbc:h2:file:${path.join(dbFolder, 'deffufa')};AUTO_SERVER=TRUE;DB_CLOSE_ON_EXIT=TRUE`
    : `jdbc:mysql://localhost:3306/deffufa`;
  let javaCmd = fs.existsSync(javaPath) ? javaPath : 'java';
  backendProcess = spawn(javaCmd, [`-Dspring.datasource.url=${jdbcUrl}`, '-jar', jarPath], { cwd: path.dirname(jarPath) });
  backendProcess.stdout.on('data', data => log(`Backend stdout: ${data.toString().trim()}`));
  backendProcess.stderr.on('data', data => log(`Backend stderr: ${data.toString().trim()}`));
  backendProcess.on('close', code => log(`Backend exited with code ${code}`));
  waitForBackendReady(BACKEND_PORT, callback);
}

// Create window
function createWindow() {
  mainWindow = new BrowserWindow({
    width: 1200, height: 800,
    webPreferences: { preload: path.join(__dirname, 'preload.js'), contextIsolation: true, nodeIntegration: false }
  });

  const indexPath = isDev
    ? path.join(__dirname, '../build', 'index.html') // dev: root-level build
    : path.join(process.resourcesPath, 'build', 'index.html'); // packaged

  mainWindow.loadURL(`file://${indexPath.replace(/\\/g, '/')}`);
  mainWindow.on('closed', () => mainWindow = null);
}

// App ready
app.whenReady().then(() => {
  if (!fs.existsSync(backendJar)) { dialog.showErrorBox('Error', `Backend JAR not found at: ${backendJar}`); app.quit(); return; }
  startBackend(backendJar, dbFolder, createWindow);
});

// Cleanup on quit
app.on('before-quit', async () => { if (mainWindow) await session.defaultSession.clearStorageData(); cleanupBackend(); });
app.on('window-all-closed', () => { if (process.platform !== 'darwin') app.quit(); });
app.on('activate', () => { if (BrowserWindow.getAllWindows().length === 0) createWindow(); });
```

---
```
cd deffufa-ui
yarn install            # install React dependencies
yarn build              # build React production files


cd ../electron
yarn install
yarn dist


$ rm -rf node_modules package-lock.json yarn.lock

```