#### [Back](./README.md)

# Prometheus

<style>
    img{
        width: 100%;
    }
</style>
![image info](./prometheus.svg)

Prometheus is an open-source monitoring and alerting toolkit originally built by SoundCloud. It has since become a popular and widely-used tool for monitoring and alerting in cloud-native environments.

## Key Features:
1. **Multi-dimensional data model:** Prometheus stores metrics as time-series data, allowing for efficient querying and aggregation.

2. **Pull-based monitoring:** Prometheus scrapes metrics from targets (e.g., applications, servers) at regular intervals.

3. **Flexible querying:** Prometheus provides a powerful query language (PromQL) for selecting and aggregating metrics.

4. **Alerting:** Prometheus integrates with Alertmanager to handle alerts and notifications.

5. **Service discovery:** Prometheus supports various service discovery mechanisms (e.g., DNS, Kubernetes) to automatically detect targets.

## Components:

1. **Prometheus Server:** The central component responsible for scraping metrics, storing data, and handling queries.

2. **Alertmanager:** Handles alerts and notifications, integrating with Prometheus to receive alerts.

3. **Pushgateway:** Allows for pushing metrics from short-lived jobs or batch processes.

4. **Exporters:** Small programs that expose metrics from applications or services to Prometheus.

## Use Cases:
1. **Monitoring cloud-native applications:** Prometheus is well-suited for monitoring microservices-based applications.

2. **Infrastructure monitoring:** Prometheus can monitor servers, networks, and other infrastructure components.

3. **Alerting and notification:** Prometheus integrates with Alertmanager to handle alerts and notifications.

## Benefits:
1. **Scalability:** Prometheus is designed to handle large-scale monitoring workloads.

2. **Flexibility:** Prometheus provides a flexible data model and query language.

3. **Integration:** Prometheus integrates with various tools and platforms (e.g., Kubernetes, Grafana).

* ### **[Prometheus Setup](./Prometheus-setup.md)**
* ### **[Prometheus Exported Setup on Ubuntu](./Prometheus-ubuntu.md)**

