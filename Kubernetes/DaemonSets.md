#### [Back](./Kubernetes-Resources.md)

# K8 DaemonSets

A DaemonSet is a type of Kubernetes deployment that ensures a specific pod runs on each machine (or a subset of machines) in a cluster. DaemonSets are useful for running system-level services, such as:
+ Logging agents
+ Monitoring agents
+ Networking services
+ Storage services

Here are some key characteristics of DaemonSets:

+ **Runs on each machine:** A DaemonSet ensures that a pod runs on each machine in the cluster.

+ **System-level services:** DaemonSets are designed for system-level services that require low-level access to the machine.

+ **No scaling:** DaemonSets do not scale like Deployments or ReplicaSets. Instead, they ensure that a pod runs on each machine.


```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: my-daemonset
spec:
  selector:
    matchLabels:
      name: my-daemonset
  template:
    metadata:
      labels:
        name: my-daemonset
    spec:
      containers:
      - name: my-container
        image: my-image:latest
  updateStrategy:
    type: RollingUpdate
```

```bash
kubectl apply -f my-daemonset.yaml
```
