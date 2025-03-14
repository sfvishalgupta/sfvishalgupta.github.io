#### [Back](./README.md)

# Imperative Vs Declarative 

## Imperative Approach

In the Imperative approach, you explicitly define the actions that need to be taken to create or modify a resource. You tell Kubernetes exactly what to do, step-by-step.

**Example**
```bash
kubectl run my-pod --image=nginx --port=80
kubectl expose pod my-pod --type=NodePort --port=80
```

In this example, you're explicitly telling Kubernetes to:
1. Create a new pod named my-pod with the nginx image.
2. Expose the pod as a NodePort service.

## Declarative Approach
In the Declarative approach, you define the desired state of the resource, and Kubernetes takes care of creating or modifying it to match that state. You tell Kubernetes what you want, and it figures out how to make it happen

**Example**
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
        image: nginx:latest
        ports:
        - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: my-app
  ports:
  - name: http
    port: 80
    targetPort: 80
  type: NodePort
```

In this example, you're defining the desired state of:
1. A deployment named my-deployment with 3 replicas.
2. A service named my-service that exposes the deployment.

Kubernetes will take care of creating or modifying the resources to match the desired state.

Key differences:

+ **Imperative:** Focuses on the steps to achieve a goal.
+ **Declarative:** Focuses on the desired outcome.
+ **Imperative:** Typically uses kubectl commands.
+ **Declarative:** Typically uses YAML or JSON configuration files.

## Imperative Commands
```bash
kubectl run --image=nginx nginx
kubectl create deployment --image=nginx nginx
kubectl expose deployment nginx --port 80
kubectl edit deployment nginx
kubectl scale deployment nginx --replicas=5
kubectl set image deployment nginx nginx=nginx:1.18
kubectl create -f nginx.yaml
kubectl replace -f nginx.yaml
kubectl delete -f nginx.yaml
```

## Declarative Commands
```bash
kubectl apply -f nginx.yaml
```