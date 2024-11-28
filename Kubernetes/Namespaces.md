#### [Back](./README.md)

# K8 Namespace

is a logical partitioning of resources and objects within a cluster

It provides a way to divide cluster resources between multiple users, teams, or applications.

### Key Characteristics of Namespaces
1. Resource isolation: Namespaces provide a scope for resources, such as pods, services, and deployments. Resources within a namespace are isolated from resources in other namespaces.
2. Resource sharing: Resources within a namespace can be shared among objects within that namespace.
3. Policy and quota management: Namespaces can have policies and quotas applied to them, controlling resource usage and access.
4. Scoping: Namespaces provide a scoping mechanism for names, allowing multiple objects with the same name to coexist in different namespaces.

### Use Cases for Namespaces
1. Multi-tenancy: Namespaces enable multiple tenants to share a single cluster, with each tenant's resources isolated from others.
2. Team or project isolation: Namespaces can be used to isolate resources for different teams or projects within an organization.
3. Development, testing, and production environments: Namespaces can be used to create separate environments for development, testing, and production.
4. Resource management: Namespaces can be used to manage resources, such as CPU and memory, for a group of objects.

### Default Namespaces
Kubernetes provides three default namespaces:
1. default: The default namespace, where objects are created if no namespace is specified.
2. kube-system: The namespace for Kubernetes system components, such as the API server and controller manager.
3. kube-public: The namespace for publicly accessible Kubernetes resources.

```bash
# Create a new namespace
kubectl create namespace my-namespace

# List all namespaces
kubectl get namespaces

# Delete a namespace
kubectl delete namespace my-namespace
```
