#### [Back](./README.md)

# K8 ConfigMaps

ConfigMaps are a Kubernetes resource that stores configuration data as key-value pairs. ConfigMaps provide a way to decouple configuration data from application code and make it easier to manage and update configuration data.

## Characteristics of ConfigMaps
Here are some key characteristics of ConfigMaps:

+ **Stores configuration data:** ConfigMaps store configuration data as key-value pairs.

+ **Decouples configuration from code:** ConfigMaps decouple configuration data from application code.

+ **Supports multiple data formats:** ConfigMaps support multiple data formats, including JSON, YAML, and properties files.

+ **Can be used with multiple applications:** ConfigMaps can be used with multiple applications.

## Types of ConfigMaps

There are two types of ConfigMaps:

1. **Literal ConfigMap:** A Literal ConfigMap is created from literal values.
2. **ConfigMap from file:** A ConfigMap can be created from a file.

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config-map
data:
  database_url: "https://my-database.com"
  api_key: "my-api-key"
```  