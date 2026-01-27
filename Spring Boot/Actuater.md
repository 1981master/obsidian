- **`/actuator/health`**: Provides application health information.
    
- **`/actuator/metrics`**: Exposes various metrics, like JVM metrics, system metrics, and custom metrics.
    
- **`/actuator/info`**: Displays application information, like version, description, and other custom details.
    
- **`/actuator/env`**: Shows environment properties.
    
- **`/actuator/loggers`**: Lets you view and modify the logging levels of your application.
    
- **`/actuator/threaddump`**: Provides a thread dump of the JVM.
    
- **`/actuator/prometheus`**: Exposes metrics in a format compatible with Prometheus.
    

There are also other endpoints like `caches`, `beans`, `scheduledtasks`, and more. You can customize which endpoints are exposed and even create your own custom endpoints

under the `/actuator` path. For example, if you hit `http://localhost:8080/actuator/health`, you might get a JSON response like this:
```json
{
  "status": "UP",
  "components": {
    "diskSpace": {
      "status": "UP",
      "details": {
        "total": 499963174976,
        "free": 1234567890,
        "threshold": 10485760
      }
    },
    "db": {
      "status": "UP",
      "details": {
        "database": "MySQL",
        "hello": 1234
      }
    }
  }
}

```

For the `metrics` endpoint at `http://localhost:8080/actuator/metrics`, you might see a JSON response like this:
`For the `metrics` endpoint at `http://localhost:8080/actuator/metrics`, you might see a JSON response like this:`'
```json
{
  "mem": {
    "count": 42,
    "total": 123456789
  },
  "jvm.memory.used": {
    "value": 123456789,
    "unit": "bytes"
  },
  // More metrics...
}

```

`And for `/prometheus`, the metrics are exposed in a Prometheus-compatible format, typically looking like:`
`# HELP jvm_memory_used_bytes The amount of memory used.
# TYPE jvm_memory_used_bytes gauge
jvm_memory_used_bytes{area="heap",id="heap-memory"} 123456789
