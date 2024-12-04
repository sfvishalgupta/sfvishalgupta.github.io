#### [Back](./Prometheus.md)

# Setup Prometheus Exporter on Ubuntu

## 1. Install Prometheus and exporters 

### * Install Prometheus:
```bash
sudo apt-get update && sudo apt-get install prometheus
```

### * Install Node Exporter (for System Matrics):
```bash
sudo apt-get install prometheus-node-exporter
```

### * Install the AWS CloudWatch Exporter (for AWS metrics):
```bash
sudo apt-get install prometheus-aws-cloudwatch-exporter
```

## 2. Configure Node Exporter
### * Create a configuration file for the Node Exporter:
```bash
sudo nano /etc/prometheus/node-exporter.conf
```

### * Add the following configuration:
```yml
global:
  scrape_interval: 10s

scrape_configs:
  - job_name: 'node'
    scrape_interval: 10s
    static_configs:
      - targets: ['localhost:9100']
```

### * Restart the Node Exporter service:
```bash
sudo service prometheus-node-exporter restart
```

## 3. Configure AWS CloudWatch Exporter

### * Create a configuration file for the AWS CloudWatch Exporter:
```bash
sudo nano /etc/prometheus/aws-cloudwatch-exporter.conf
```

### * Add the following configuration:
```yml
global:
  scrape_interval: 10s

scrape_configs:
  - job_name: 'aws-cloudwatch'
    scrape_interval: 10s
    static_configs:
      - targets: ['localhost:9401']
    metrics_path: /aws-cloudwatch
    params:
      access_key_id: [YOUR_ACCESS_KEY_ID]
      secret_access_key: [YOUR_SECRET_ACCESS_KEY]
      region: [YOUR_REGION]
```

### * Restart the AWS CloudWatch Exporter service:
```bash
sudo service prometheus-aws-cloudwatch-exporter restart
```

## 4. Configure Prometheus

### * Create a configuration file for Prometheus:
```bash
sudo nano /etc/prometheus/prometheus.yml
```

### * Add the following configuration:
```yml
global:
  scrape_interval: 10s

scrape_configs:
  - job_name: 'node'
    scrape_interval: 10s
    static_configs:
      - targets: ['localhost:9100']
  - job_name: 'aws-cloudwatch'
    scrape_interval: 10s
    static_configs:
      - targets: ['localhost:9401']
```

### * Restart the Prometheus service:
```bash
sudo service prometheus restart
```

## 5. Verify the exporter
### * Verify that the Node Exporter is scraping metrics:
```bash
curl http://localhost:9100/metrics
```

### * Verify that the AWS CloudWatch Exporter is scraping metrics:
```bash
curl http://localhost:9401/metrics
```

### * Verify that Prometheus is scraping metrics from both exporters:
```bash
curl http://localhost:9090/metrics
```
