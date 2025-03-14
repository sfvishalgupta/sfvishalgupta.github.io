#### [Back](./Kubernetes-Resources.md)

# K8 Storage Classes

A StorageClass is a Kubernetes resource that defines a type of storage that can be provisioned and managed by Kubernetes. StorageClasses provide a way to define different types of storage, such as SSD, HDD, or cloud-based storage.

## Characteristics of StorageClass

Here are some key characteristics of StorageClass:
+ **Defines storage type:** StorageClasses define a type of storage, such as SSD or HDD.

+ **Provisioning:** StorageClasses can provision storage resources dynamically.

+ **Parameters:** StorageClasses can define parameters, such as storage size or access mode.

+ **Reclaim policy:** StorageClasses can define a reclaim policy, which determines what happens to the storage resource when it is released.

## Types of StorageClass

There are several types of StorageClass:

1. **Static StorageClass:** Static StorageClass is used to provision storage resources that already exist.

2. **Dynamic StorageClass:** Dynamic StorageClass is used to provision storage resources dynamically.

```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: my-storage-class
provisioner: kubernetes.io/aws-ebs
parameters:
  type: gp2
  zones: us-west-2a, us-west-2b
reclaimPolicy: Retain
allowVolumeExpansion: true
```