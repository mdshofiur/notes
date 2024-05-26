# Prometheus and grafana monitoring for .net application

## Setting up Docker Compose

```yaml
version: '3.8'

services:
   # prometheus
   prometheus:
      image: prom/prometheus:latest
      container_name: prometheus
      command:
         - '--config.file=/etc/prometheus/prometheus.yml'
         - '--storage.tsdb.path=/prometheus'
         - '--web.console.libraries=/etc/prometheus/console_libraries'
         - '--web.console.templates=/etc/prometheus/consoles'
         - '--web.enable-lifecycle'
      volumes:
         - ./prom/prometheus.yml:/etc/prometheus/prometheus.yml
         - ./data:/prometheus
      ports:
         - '9090:9090'
      environment:
         - 'TZ=UTC'

   # grafana
   grafana:
      image: grafana/grafana:latest
      container_name: grafana
      ports:
         - '3000:3000'
      volumes:
         - ./grafana-data/data:/var/lib/grafana
         - ./grafana-data/provisioning:/etc/grafana/provisioning
         - ./grafana:/etc/grafana/provisioning/datasources
      environment:
         - GF_SECURITY_ADMIN_USER=admin
         - GF_SECURITY_ADMIN_PASSWORD=admin
         - GF_USERS_ALLOW_SIGN_UP=false
         
    # aspdotnet
   aspdotnet:
      image: shafikur/aspdotnet-app:latest
      container_name: aspdotnet
      ports:
         - '8080:8080'
```

## Installing prometheus


```
dotnet add package prometheus-net.AspNetCore
```

## Configuring prometheus in Program.cs

```
using Prometheus;

   app.UseRouting();
   app.UseHttpMetrics();

   app.MapMetrics();
```

## prometheus.yml Configuration

```
global:
  scrape_interval: 15s
  scrape_timeout: 10s
  evaluation_interval: 15s
alerting:
  alertmanagers:
    - scheme: http
      timeout: 10s
      api_version: v1
      static_configs:
        - targets: []
scrape_configs:
  - job_name: dotnet application
    honor_timestamps: true
    scrape_interval: 15s
    scrape_timeout: 10s
    metrics_path: /metrics
    scheme: http
    static_configs:
      - targets:
          - host.docker.internal:8080
  - job_name: prometheus
    static_configs:
      - targets: ['localhost:9090']
```

## Go to Grafana: http://localhost:3000/
Log in with username and password ‘admin’, after that, and add a new data source connection:--

Click on ‘Add new Data Source’ in the ‘Connection’ set the Prometheus URL: “http://prometheus:9090” (this is our container name)




