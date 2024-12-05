#### [Back](../Deployments.md)

# Rolling Update Deployment Strategy

A Rolling Update in Kubernetes is a deployment strategy that allows you to update a running application with new versions of containers, configuration, or other application components, without downtime or interruption to users.

In this strategy, the new version of the application is deployed in a rolling update fashion, where one pod at a time is updated.

+ **Pros:** Zero downtime, easy to manage.
+ **Cons:** Can be slow for large deployments.

### **How Rolling Updates Work**

Here's a step-by-step overview of the Rolling Update process:

1. **Update the Deployment Configuration:** You update the deployment configuration, such as the container image, environment variables, or other settings.

2. **Kubernetes Creates a New ReplicaSet:** Kubernetes creates a new ReplicaSet with the updated configuration.

3. **New Pods are Created:** The new ReplicaSet creates new pods with the updated configuration.

4. **Old Pods are Terminated:** The old pods are terminated, and the new pods take their place.

5. **Rolling Update is Complete:** Once all old pods are terminated and replaced with new pods, the Rolling Update is complete.

### Benefits of Rolling Updates

Rolling Updates provide several benefits:

+ **Zero Downtime:** Rolling Updates allow you to update your application without downtime or interruption to users.

+ **Flexibility:** Rolling Updates enable you to update individual components of your application, such as containers or configuration, without affecting the entire application.

+ **Easy Rollbacks:** If something goes wrong during the update, Rolling Updates make it easy to roll back to a previous version.

### Example yaml template for Rolling Update
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
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
```

