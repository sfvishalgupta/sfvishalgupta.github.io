#### [Back](./Kubernetes-Resources.md)

# K8 CronJobs

To run a CronJob in Kubernetes (k8), you'll need to create a YAML or JSON file that defines the CronJob. Here's an example of a simple CronJob that runs a container every minute:

```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: my-cronjob
spec:
  schedule:
    - cron: */1 * * * *
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: my-container
            image: my-image:latest
            command: ["echo", "Hello, World!"]
          restartPolicy: OnFailure
  successfulJobsHistoryLimit: 3
  failedJobsHistoryLimit: 1
```  

```bash
kubectl apply -f my-cronjob.yaml
```