#### [Back](../Deployments.md)

# Blue-Green Deployment Strategy

In this strategy, two environments are maintained: Blue (current production environment) and Green (new version of the application). Traffic is routed to the Green environment once it's verified to be working correctly.

+ **Pros:** Zero downtime, easy to roll back.

+ **Cons:** Requires double the resources

## Example Blue-Green Deployment Strategy

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: blue-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: blue-app
  template:
    metadata:
      labels:
        app: blue-app
    spec:
      containers:
      - name: blue-container
        image: blue-image:latest
        ports:
        - containerPort: 80

---

apiVersion: apps/v1
kind: Deployment
metadata:
  name: green-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: green-app
  template:
    metadata:
      labels:
        app: green-app
    spec:
      containers:
      - name: green-container
        image: green-image:latest
        ports:
        - containerPort: 80
```