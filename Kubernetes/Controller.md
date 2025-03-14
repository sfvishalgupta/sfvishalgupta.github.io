#### [Back](./README.md)

# K8 Controllers

In Kubernetes, controllers are control plane components that manage the state of the cluster. They ensure that the cluster's current state matches the desired state.

Here are some of the main Kubernetes controllers:

### 1. ReplicaSet Controller:
Ensures that a specified number of replicas (i.e., copies) of a pod are running at any given time.

### 2. ReplicationController (RC) Controller: 
Similar to ReplicaSet, but older and less flexible.

### 3. Deployment Controller: 
Manages rollouts and rollbacks of pods and ReplicaSets.

### 4. DaemonSet Controller: 
Ensures that a specific pod runs on each machine in the cluster.

### 5. Job Controller: 
Manages batch processing workloads, ensuring that a specified number of pods complete successfully.

### 6. CronJob Controller: 
Similar to Job, but for periodic execution of tasks.

### 7. StatefulSet Controller: 
Manages stateful applications, ensuring that each pod has a unique identity and persistent storage.

### 8. Persistent Volume (PV) Controller: 
Manages persistent storage resources, ensuring that they are properly provisioned and bound to pods.

### 9. Service Controller: 
Manages services, ensuring that they are properly exposed and load-balanced.

### 10. Endpoint Controller: 
Manages endpoint resources, ensuring that they are properly updated and synchronized with services.

### 11. Namespace Controller: 
Manages namespace resources, ensuring that they are properly created, updated, and deleted.

### 12. ResourceQuota Controller: 
Manages resource quotas, ensuring that namespaces do not exceed their allocated resources.

These controllers work together to ensure that the cluster is running smoothly and efficiently.