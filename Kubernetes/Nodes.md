#### [Back](./Kubernetes-Resources.md)

# K8 Nodes

A Node is a machine (physical or virtual) that participates in a Kubernetes cluster. Nodes are the workers that run the applications and provide the computational resources.

## Types of Nodes
1. **Master Node:** The master node is responsible for managing the cluster, including scheduling, scaling, and upgrading. It runs the Kubernetes control plane components, such as the API server, controller manager, and scheduler.

2. **Worker Node:** Worker nodes are responsible for running the applications. They execute the tasks assigned by the master node and provide the computational resources.

3. **Etcd Node:** Etcd is a distributed key-value store that stores the cluster's configuration and state. Etcd nodes are responsible for storing and replicating the data.

## Node Components
1. **Kubelet:** The Kubelet is an agent that runs on each node and manages the node's resources, such as CPU, memory, and storage.

2. **Kube-proxy:** The Kube-proxy is a network proxy that runs on each node and manages the node's network traffic.

3. **Container Runtime:** The container runtime is responsible for running the containers on the node. Examples of container runtimes include Docker, rkt, and cri-o.

## Node Roles
1. **Master:** The master role is responsible for managing the cluster.
2. **Worker:** The worker role is responsible for running the applications.
3. **Etcd:** The etcd role is responsible for storing and replicating the cluster's data.

## Node Status
1. **Ready:** The node is ready to accept new pods.
2. **NotReady:** The node is not ready to accept new pods.
3. **Unknown:** The node's status is unknown.

## Node Management
1. **Adding Nodes:** New nodes can be added to the cluster using the kubectl join command.

2. **Removing Nodes:** Nodes can be removed from the cluster using the kubectl drain and kubectl delete node commands.

3. **Upgrading Nodes:** Nodes can be upgraded using the kubectl upgrade command.

4. **Maintaining Nodes:** Nodes can be maintained using the kubectl describe node and kubectl get node commands.

## Node Affinity

Type
+ **requiredDuringSchedulingIgnoredDuringExecution**

+ **prefferedDuringSchedulingIgnoredDuringExecution**

To put the POD at Node Having Label **Large**
```yaml
spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
            - key: size
              operator: in
              values:
              - Large
```

is Equvalent to 

```yaml
nodeSelector:
    size: Large
```

## Lable a Node (For Node Selector)
```bash
kubectl lable nodes node app-node size=large
```

## Get Taints on Node
```bash
kubectl describe node node01 | grep Taints
```

## K8 Drain
The drain command is used to safely evict all pods from a node, typically before performing maintenance or decommissioning the node.
When you run k8 drain <node_name>, Kubernetes will:

1. Mark the node as unschedulable (i.e., no new pods will be scheduled on it).
2. Evict all pods from the node, respecting the PodDisruptionBudget (if defined).
3. Wait for the pods to be deleted or rescheduled on other nodes.

## k8 cordon
The cordon command is used to mark a node as unschedulable, preventing new pods from being scheduled on it.
When you run k8 cordon <node_name>, Kubernetes will:
1. Mark the node as unschedulable.
2. Prevent new pods from being scheduled on the node.
Note that existing pods on the node will not be affected.

## k8 uncordon:
The uncordon command is used to mark a node as schedulable again, allowing new pods to be scheduled on it.
When you run k8 uncordon <node_name>, Kubernetes will:
1. Mark the node as schedulable.
2. Allow new pods to be scheduled on the node.

```bash
# Mark a node as unschedulable (cordon)
k8 cordon my-node

# Drain a node (evict all pods)
k8 drain my-node

# Mark a node as schedulable again (uncordon)
k8 uncordon my-node
```