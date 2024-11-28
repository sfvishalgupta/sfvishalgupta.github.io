#### [Back](./README.md)

# K8 ReplicaSets

Ensure a specified number of replicas(identical pods) are running at any given time.

Managing ReplicaSets in Kubernetes involves creating, scaling, updating, and deleting them.

## Creating a ReplicaSet

You can create a ReplicaSet using a YAML or JSON configuration file.

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: my-replica-set
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
```

Apply the configuration file using:-

```bash
kubectl apply -f my-replica-set.yaml
```

## Scaling a ReplicaSet
You can scale a ReplicaSet using the kubectl scale command:

```bash
kubectl scale replicaset my-replica-set --replicas=5
```

Alternatively, you can update the replicas field in the ReplicaSet configuration file and apply the changes:

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: my-replica-set
spec:
  replicas: 5
  ...
```

```bash
kubectl apply -f my-replica-set.yaml
```

## Updating a ReplicaSet
To update a ReplicaSet, you can modify the configuration file and apply the changes:

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: my-replica-set
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
        image: nginx:1.19
```
```bash
kubectl apply -f my-replica-set.yaml
```

## Deleting a ReplicaSet
To delete a ReplicaSet, use the kubectl delete command:
```bash
kubectl delete replicaset my-replica-set
```

Alternatively, you can use the --cascade flag to delete the ReplicaSet and its associated Pods:

```bash
kubectl delete replicaset my-replica-set --cascade=true
```


## ReplicaSet Status
```bash
kubectl get replicaset my-replica-set
```