#### [Back](./Prometheus.md)

# Setup Prometheus

## 1. **Install Prometheus** 
```bash
brew install prometheus
```

## 2. **Start the Service** 
```bash
brew services start prometheus
brew services list
```

## 3. **Verify Prometheus**
```bash
brew services list
```

## 4. **Access the Prometheus web interface**
```bash
http://localhost:9090
```

## 5. **Updating the config file**

```bash
code /opt/homebrew/etc/prometheus.yml
```

**Add below code to scrap config like**
```yaml
- job_name: 'new-server'
  scrape_interval: 10s
  static_configs:    
  - targets: ['1.2.3.4:9100']
```

**Restart Prometheus Service**
```bash
brew services restart prometheus
```
