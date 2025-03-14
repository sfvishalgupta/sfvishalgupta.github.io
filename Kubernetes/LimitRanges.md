#### [Back](./Kubernetes-Resources.md)

# K8 Limit Ranges

In Kubernetes, a **LimitRange** is a resource that defines the constraints on the resources that can be requested or used by containers in a namespace.

A LimitRange provides a way to:

1. **Enforce resource limits:** Ensure that containers do not consume excessive resources, such as CPU or memory.

2. **Set default resource requests:** Provide default resource requests for containers that do not specify their own resource requests.

A LimitRange consists of the following:

1. **Limits:** Define the maximum amount of resources that can be used by containers.
2. **Requests:** Define the minimum amount of resources that are guaranteed to be available to containers.

LimitRange can be applied to:
1. **Pods:** LimitRange can be applied to pods, which will enforce the limits on all containers within the pod.

2. **Containers:** LimitRange can be applied to individual containers, which will enforce the limits only on that container.

Here is an example of a LimitRange:
```yaml
apiVersion: v1
kind: LimitRange
metadata:
  name: my-limit-range
spec:
  limits:
  - type: Container
    max:
      cpu: 2
      memory: 1Gi
    min:
      cpu: 100m
      memory: 128Mi
```

In this example, the LimitRange defines:

+ **Maximum CPU limit:** 2 cores
+ **Maximum memory limit:** 1 GB
+ **Minimum CPU request:** 100 millicores
+ **Minimum memory request:** 128 MB

# K8 Resource Quota (on Namespace)

In Kubernetes, a ResourceQuota is a resource that defines the constraints on the resources that can be used by objects in a namespace.

A ResourceQuota provides a way to:

1. **Enforce resource limits:** Ensure that the total resources used by objects in a namespace do not exceed the defined limits.

2. **Manage resource utilization:** Control the amount of resources used by objects in a namespace, preventing overcommitment and ensuring efficient resource utilization.

A ResourceQuota can be used to limit the following resources:
1. **CPU:** Limit the total CPU resources used by objects in a namespace.

2. **Memory:** Limit the total memory resources used by objects in a namespace.

3. **Storage:** Limit the total storage resources used by objects in a namespace.

4. **Pods:** Limit the total number of pods that can be created in a namespace.

Here is an example of a ResourceQuota:

```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: my-quota
spec:
  hard:
    cpu: 2
    memory: 1Gi
    pods: 10
  scope:
    - Terminating
    - NotTerminating
```

In this example, the ResourceQuota defines:
+ **CPU limit:** 2 cores
+ **Memory limit:** 1 GB
+ **Pod limit:** 10 pods
+ **Scope:** Applies to terminating and not-terminating pods

By creating a ResourceQuota, you can ensure that the resources used by objects in a namespace are within the defined limits, preventing overcommitment and ensuring efficient resource utilization.

