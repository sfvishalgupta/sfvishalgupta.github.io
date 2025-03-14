#### [Back](./README.md)

# Installing Kubernetes

1. **Using Kubernetes in Docker (KIND)**

```bash
brew install kind
```

2. **Creating a Cluster**
```bash
kind delete cluster -n cluster_name
kind create cluster --config kind.yaml  # Creating a Cluster
```

Below is the config file for creating a cluster with extra mount option

```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
name: kc-cluster
nodes:
- role: control-plane
  extraMounts:
  - hostPath: /var/www/kubernetes/data
    containerPath: /mnt/data
```

3. **Get Clusters**
```bash
kind get clusters       # List of Clusters
kind get nodes          # List of Nodes
kind get kubeconfigs    # List all config
```

3. **Install Kubectl**
```bash 
brew install kubectl
```

Containers -> Nodes (Machine) -> PODS

1. A Cluster is a group of [Nodes](./Nodes.md).
2. A Node is a machine that runs [Pods](./Pods.md).
3. A [Pods](./Pods.md) is a logical host for one or more containers.
