#### [Back](./README.md)

# K8 Ingress

Ingress is a Kubernetes resource that provides a simple way to manage access to services running in a cluster. It acts as an entry point for incoming HTTP requests, allowing you to:

+ **Expose services:** Make services accessible to the outside world.
Route traffic: Route incoming requests to the correct service based on the request URL, host, or headers.

+ **Provide SSL/TLS termination:** Terminate SSL/TLS connections and decrypt traffic before forwarding it to the service.

+ **Support URL rewriting:** Rewrite URLs to match the requirements of the service.

## Ingress Components
An Ingress resource consists of the following components:

1. **Ingress Controller:** Responsible for implementing the Ingress resource and managing the routing of incoming requests.

2. **Ingress Rules:** Define the routing rules for incoming requests, including the host, path, and backend service.

3. **Backend Services:** The services that receive traffic from the Ingress Controller.

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-ingress
spec:
  rules:
  - host: myapp.example.com
    http:
      paths:
      - path: /
        backend:
          serviceName: my-service
          servicePort: 80
```

```bash
kubectl apply -f my-ingress.yaml
```