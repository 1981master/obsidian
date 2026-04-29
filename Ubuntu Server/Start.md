
# 🖥 1️⃣ Install Linux on the Laptop

### Recommended OS:

- **Ubuntu Server** (best for servers, lightweight)
    
- Or **Ubuntu** if you prefer a GUI
    

👉 Download from: [https://ubuntu.com/download](https://ubuntu.com/download)

During installation:

- Enable **OpenSSH server** (important for remote access)
    
- Create a strong username/password
    

After install:

sudo apt update && sudo apt upgrade -y

---

# 🌐 2️⃣ Give the Server a Static IP (Very Important)

You want your laptop server to always have the same local IP.

Option A (Easy):

- Set static IP in your router DHCP settings
    

Option B (Manual in Ubuntu):  
Edit netplan config:

sudo nano /etc/netplan/00-installer-config.yaml

---

# ☕ 3️⃣ Install Java for Spring Boot

Check your Spring Boot Java version (usually 17 or 21).

Install OpenJDK:

sudo apt install openjdk-17-jdk -y

Verify:

java -version

---

# 📦 4️⃣ Build and Deploy Spring Boot App

On your development machine:

./mvnw clean package

This creates:

target/yourapp.jar

Copy it to server:

scp target/yourapp.jar user@server-ip:/home/user/

Run it:

java -jar yourapp.jar

Now backend runs on:

http://server-ip:8080

---

# ⚛ 5️⃣ Build React App for Production

Inside your React project:

npm run build

This creates a `build/` folder.

You now have two options:

---

## Option A (Simple): Serve React with Nginx (Recommended)

Install:

sudo apt install nginx -y

Remove default config:

sudo rm -rf /var/www/html/*

Copy React build:

sudo cp -r build/* /var/www/html/

Now React app works at:

http://server-ip

---

# 🔁 6️⃣ Connect React to Spring Boot

Inside React:

axios.get("http://server-ip:8080/api/endpoint")

For production, better use Nginx reverse proxy 👇

---

# 🚀 7️⃣ Setup Nginx Reverse Proxy (Professional Setup)

Edit:

sudo nano /etc/nginx/sites-available/default

Example config:

server {  
    listen 80;  
  
    location / {  
        root /var/www/html;  
        index index.html;  
        try_files $uri /index.html;  
    }  
  
    location /api/ {  
        proxy_pass http://localhost:8080/;  
    }  
}

Restart:

sudo systemctl restart nginx

Now:

- Frontend → `http://server-ip`
    
- Backend → `http://server-ip/api/...`
    

---

# 🔥 8️⃣ Open Firewall

Enable UFW:

sudo ufw allow 80  
sudo ufw allow 22  
sudo ufw enable

---

# 🔄 9️⃣ Make Spring Boot Run Automatically

Install **systemd** service.

Create file:

sudo nano /etc/systemd/system/myapp.service

Add:

[Unit]  
Description=Spring Boot App  
After=network.target  
  
[Service]  
User=youruser  
ExecStart=/usr/bin/java -jar /home/youruser/yourapp.jar  
SuccessExitStatus=143  
Restart=always  
RestartSec=5  
  
[Install]  
WantedBy=multi-user.target

Enable:

sudo systemctl daemon-reload  
sudo systemctl enable myapp  
sudo systemctl start myapp

Now it auto-starts on reboot ✅

---

# 🌍 10️⃣ Make It Public (Optional)

If you want internet access:

1. Port forward 80 on router → server IP
    
2. Use a free domain:
    
    - **No-IP**
        
    - **DuckDNS**
        

For HTTPS:

sudo apt install certbot python3-certbot-nginx

Then:

sudo certbot --nginx

---

# 🧠 Better Alternative (Advanced)

You can use:

- **Docker**
    
- **Docker Compose**
    

This makes deployment MUCH cleaner and professional.

If you want, I can show you full Docker setup for Spring Boot + React.

---

# ⚡ Realistic Expectations for Old Laptop

Works well for:

- Portfolio projects
    
- Internal tools
    
- Learning DevOps
    
- Small traffic apps
    

Not ideal for:

- High traffic production
    
- Critical business apps
    

---

# 🏁 Final Architecture (Recommended)

Internet  
   ↓  
Router Port Forward  
   ↓  
Nginx (Port 80/443)  
   ↓  
Spring Boot (Port 8080)  
   ↓  
Database (PostgreSQL/MySQL)

---

If you'd like, tell me:

- How much RAM your laptop has
    
- Which Java version you use
    
- Whether you want Docker or not
    

And I’ll give you a more optimized setup 🔥

Attach

Voice