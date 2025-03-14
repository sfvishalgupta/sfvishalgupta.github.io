#### [Back](./Kubernetes-Resources.md)

# K8 ResourceQuota

In Kubernetes, a ResourceQuota is a resource that defines a set of constraints on the resources that can be consumed by a namespace or a set of namespaces.

## Why ResourceQuota?

ResourceQuota helps to:
1. **Prevent overcommitment:** Ensure that a namespace or a set of namespaces does not consume more resources than allocated.

2. **Enforce resource limits:** Define limits on the resources that can be consumed by a namespace or a set of namespaces.

3. **Provide resource isolation:** Isolate resources between namespaces or sets of namespaces.

## Types of ResourceQuota:

1. **Compute ResourceQuota:** Defines limits on compute resources such as CPU and memory.

2. **Storage ResourceQuota:** Defines limits on storage resources such as persistent volumes.

3. **Object Count ResourceQuota:** Defines limits on the number of objects such as pods, services, and deployments.

## Creating a ResourceQuota:
You can create a ResourceQuota using a YAML or JSON file:

```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: my-quota
spec:
  hard:
    pods: 10
    request.cpu: 1000m
    request.memory: 512Mi
    limits.cpu: "10"
    limits.memory: 10Gi
  scope:
    - Namespace
```

in this example, the ResourceQuota defines limits on CPU and memory resources for a namespace.

## Assigning a ResourceQuota:
You can assign a ResourceQuota to a namespace using the kubectl command:
```bash
kubectl create namespace my-namespace
kubectl create resourcequota my-quota -n my-namespace
```

In this example, the ResourceQuota my-quota is assigned to the namespace my-namespace.
