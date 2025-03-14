#### [Back](./Kubernetes-Resources.md)

# K8 StatefulSets 

Kubernetes (K8) StatefulSets are a type of deployment that manages stateful applications. Unlike Deployments, which manage stateless applications, StatefulSets provide guarantees about the ordering and uniqueness of pods.

## Characteristics of StatefulSets

Here are some key characteristics of StatefulSets:
+ **Ordered deployment and scaling:** StatefulSets deploy and scale pods in a specific order, ensuring that each pod is assigned a unique and persistent identity.

+ **Persistent storage:** StatefulSets provide persistent storage for each pod, allowing data to be retained even if a pod is deleted or recreated.

+ **Network identity:** Each pod in a StatefulSet is assigned a unique network identity, including a hostname and IP address.

## Use cases for StatefulSets
StatefulSets are suitable for applications that require:

+ **Persistent data:** Applications that require data to be persisted across pod restarts or scaling events.

+ **Ordered deployment:** Applications that require a specific deployment order, such as a primary-secondary database setup.

+ **Unique network identity:** Applications that require a unique network identity for each pod, such as a distributed database.

```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: my-statefulset
spec:
  replicas: 3
  serviceName: "my-service"
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-container
        image: my-image:latest
        volumeMounts:
        - name: my-volume
          mountPath: /data
  volumeClaimTemplates:
  - metadata:
      name: my-volume
    spec:
      accessModes: [ "ReadWriteOnce" ]
      resources:
        requests:
          storage: 1Gi
```          

## Example for Postgresql
```yml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: postgres-statefulset
spec:
  replicas: 1
  selector:
    matchLabels:
      app: postgres
  serviceName: "postgres-svc"
  template:
    metadata:
      labels:
        app: postgres
    spec:
      containers:
      - name: postgres
        image: postgres:13
        ports:
        - containerPort: 5432
        env:
        - name: POSTGRES_USER
          value: "myuser"
        - name: POSTGRES_PASSWORD
          value: "mypassword"
        - name: POSTGRES_DB
          value: "mydb"
        volumeMounts:
        - name: postgres-persistent-storage
          mountPath: /var/lib/postgresql/data
  volumeClaimTemplates:
  - metadata:
      name: postgres-persistent-storage
    spec:
      accessModes: ["ReadWriteOnce"]
      resources:
        requests:
          storage: 1Gi
```