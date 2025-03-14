#### [Back](./README.md)

# K8 Taints & Tolerations

In Kubernetes (K8), **Taints and Tolerations** are mechanisms that allow you to control the scheduling of pods on nodes.

## Taints:
A Taint is a way to mark a node as having a specific condition or limitation that might affect the pods running on it. Taints are key-value pairs that are applied to a node.

There are three types of taints:

1. **NoSchedule:** Pods will not be scheduled on the node.

2. **PreferNoSchedule:** The scheduler will try to avoid scheduling pods on the node, but it's not guaranteed.

3. **NoExecute:** Existing pods on the node will be evicted, and new pods will not be scheduled.

## Tolerations:
A Toleration is a way to specify that a pod can tolerate a specific taint on a node. Tolerations are also key-value pairs that are applied to a pod.
When a pod has a toleration, it can be scheduled on a node with a matching taint.

### Example:
Suppose you have a node with a taint:
```yaml
apiVersion: v1
kind: Node
metadata:
  name: node1
spec:
  taints:
  - key: "gpu"
    value: "true"
    effect: "NoSchedule"
```

You can create a pod with a toleration to schedule it on this node:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
  - name: my-container
    image: my-image
  tolerations:
  - key: "gpu"
    operator: "Equal"
    value: "true"
    effect: "NoSchedule"
```

In this example, the pod my-pod has a toleration for the gpu taint on the node node1. The pod can be scheduled on this node despite the taint.
Taints and tolerations provide a flexible way to manage node constraints and pod scheduling in Kubernetes.