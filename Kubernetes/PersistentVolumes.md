#### [Back](./README.md)

# K8 Persistent Volumes (PVs)
Persistent Volumes are a Kubernetes resource that provides persistent storage for pods. PVs are used to manage storage resources, such as disks or files, that are required by pods.

## Characteristics of Persistent Volumes
Here are some key characteristics of Persistent Volumes:

+ **Persistent storage:** PVs provide persistent storage for pods, allowing data to be retained even if a pod is deleted or recreated.

+ **Decoupling storage from pods:** PVs decouple storage from pods, allowing storage resources to be managed independently of pods.

+ **Dynamic provisioning:** PVs support dynamic provisioning, allowing storage resources to be created and deleted automatically.

## Types of Persistent Volumes
There are two types of Persistent Volumes:

1. **Static PVs:** Static PVs are manually created by administrators and are not dynamically provisioned.

2. **Dynamic PVs:** Dynamic PVs are created automatically by Kubernetes when a Persistent Volume Claim (PVC) is created.


## Persistent Volume Components
A Persistent Volume consists of the following components:

1. **Persistent Volume (PV):** The PV is the storage resource itself.

2. **Persistent Volume Claim (PVC):** The PVC is a request for storage resources.

3. **StorageClass:** The StorageClass defines the type of storage resources that can be created.

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: my-pv
spec:
  capacity:
    storage: 5Gi
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  storageClassName: my-storage-class
  local:
    path: /mnt/data
  nodeAffinity:
    required:
      nodeSelectorTerms:
      - matchExpressions:
        - key: kubernetes.io/hostname
          operator: In
          values:
          - my-node
```          