#### [Back](./README.md)

# AWS List of all Lambdas

```bash 
aws lambda list-functions --region us-east-1 --query 'Functions[*].[FunctionName]' --output text 
```