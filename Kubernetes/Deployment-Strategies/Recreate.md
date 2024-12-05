#### [Back](../Deployments.md)

# Recreate Deployment Strategy

In this strategy, the old version of the application is terminated, and then the new version is deployed.

+ **Pros:** Simple to implement, easy to manage.

+ **Cons:** Downtime is experienced during the deployment process.

## Example of Recreate Deployment Strategy
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-container
        image: my-image:latest
        ports:
        - containerPort: 80
  strategy:
    type: Recreate
```