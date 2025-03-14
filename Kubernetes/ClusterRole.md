#### [Back](./Kubernetes-Resources.md)

# K8 ClusterRole & ClusterRoleBinding

## ClusterRoles:
A ClusterRole is a set of permissions that can be applied to a user or a service account. ClusterRoles define what actions can be performed on cluster-wide resources, such as:
+ Nodes
+ Persistent Volumes
+ Namespaces
+ Pods

ClusterRoles are defined using a YAML or JSON file that specifies the permissions and the resources they apply to.

### Example of a ClusterRole:

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: cluster-admin
rules:
- apiGroups: ["*"]
  resources: ["*"]
  verbs: ["*"]
```

## ClusterRoleBindings:
A ClusterRoleBinding is used to bind a ClusterRole to a user or a service account. This binding grants the permissions defined in the ClusterRole to the user or service account.

ClusterRoleBindings are defined using a YAML or JSON file that specifies the ClusterRole and the user or service account to bind it to.

### Example of a ClusterRoleBinding:
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: cluster-admin-binding
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- apiGroup: rbac.authorization.k8s.io
  kind: User
  name: admin
```

In summary:
+ **ClusterRoles define permissions for cluster-wide resources.**

+ **ClusterRoleBindings bind ClusterRoles to users or service accounts, granting them the defined permissions.**

## Test the ClusterRoleBinding

```yaml
kubectl get pods --as admin
```