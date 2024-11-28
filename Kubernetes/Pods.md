#### [Back](./README.md)

# K8 Pods

In Kubernetes (k8), a Pod is the basic execution unit of a containerized application. It's the smallest and simplest unit of deployment, scaling, and management.

## What is a Pod? ##
A Pod represents a single instance of a running application. 
It's a logical host for one or more containers. Containers within a Pod share the 
same network namespace, IP address, and port space.

## Key Characteristics of Pods ##
1. **One or more containers:** A Pod can contain one or more containers.
2. **Shared network namespace:** Containers within a Pod share the same network namespace.
3. **Shared IP address:** Containers within a Pod share the same IP address.
4. **Shared port space:** Containers within a Pod share the same port space.
5. **Ephemeral:** Pods are ephemeral, meaning they can be created, scaled, and deleted as needed.
6. **Managed by Kubernetes:** Pods are managed by the Kubernetes control plane.

## Pod Components
1. **Container(s):** One or more containers running within the Pod.
2. **Pause container:** A special container that runs in the background to keep the Pod alive.
3. **Network namespace:** The shared network namespace for the containers within the Pod.
4. **Volumes:** Persistent storage volumes attached to the Pod.

## Pod Lifecycle
1. **Pending:** The Pod is created and is waiting for resources to be allocated.
2. **Running:** The Pod is running and at least one container is in the running state.
3. **Succeeded:** The Pod has completed its execution and all containers have terminated successfully.
4. **Failed:** The Pod has failed and at least one container has terminated with a non-zero exit code.
5. **Unknown:** The Pod's status is unknown.

## Pod Types
1. **ReplicaSet Pod:** A Pod managed by a ReplicaSet.
2. **Deployment Pod:** A Pod managed by a Deployment.
3. **StatefulSet Pod:** A Pod managed by a StatefulSet.
4. **DaemonSet Pod:** A Pod managed by a DaemonSet.

## Create a POD

```bash
kubectl create -f my-pod.yaml
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-app-pod
  namespace: dev
spec:
  containers:
  - name: ubuntu
    image: ubuntu:latest
```

## Connect to a POD
```bash
kubectl exec -it ubuntu-pod -- bash
```

## List of Pods
```bash
kubectl get pods --namespace dev
```

## Delete Pod
```bash
kubectl delete pod 
```

