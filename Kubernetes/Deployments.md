#### [Back](./README.md)

# K8 Deployments

A Kubernetes (k8) deployment is a way to describe the desired state of a pod or group of pods in a Kubernetes cluster. It provides a declarative way to manage the deployment and scaling of applications.

Here are some key aspects of a Kubernetes deployment:
## Characteristics
+ **Declarative configuration:** You describe what you want to deploy and how it should be deployed.

+ **Replica management:** Deployments manage multiple replicas (i.e., copies) of a pod to ensure high availability.

+ **Rollouts and rollbacks:** Deployments support rolling updates and rollbacks to previous versions.

+ **Self-healing:** If a pod crashes or becomes unresponsive, the deployment will automatically replace it.

## Deployment Manifest
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
```

## Benefits
Kubernetes deployments provide several benefits, including:

+ **Easy rollouts and rollbacks:** Deployments make it simple to roll out new versions of an application and roll back to previous versions if needed.

+ **High availability:** Deployments ensure that a specified number of replicas are running at all times, making it easier to achieve high availability.

+ **Simplified management:** Deployments provide a simple way to manage complex applications, making it easier to scale, update, and manage your applications.

## Scaling Deployments
To update the number of replicas in a Kubernetes deployment, you can use **scale** 

1. **Update Replicas Using kubectl scale**
```bash
kubectl scale deployment my-deployment --replicas=5
```

2. **Update Replicas Using kubectl patch**
```bash
kubectl patch deployment my-deployment -p '{"spec":{"replicas":5}}'
```

3. **Verify the Update**
```bash
kubectl get deployment my-deployment -o yaml
```

## Deployment Stratigies

1. **[Recreate Deployment Strategy](./Deployment-Strategies/Recreate.md)**
2. **[Rolling Update Deployment Strategy (Default)](./Deployment-Strategies/Rolling-Update.md)**
3. **[Blue-Green Deployment Strategy](./Deployment-Strategies/Blue-Green.md)**
4. **[Canary Deployment Strategy](./Deployment-Strategies/Canary.md)**
5. **[A/B Testing Deployment Strategy](./Deployment-Strategies/A-B-Testing.md)**

