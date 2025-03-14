#### [Back](./Kubernetes-Resources.md)

# K8 Secrets

Kubernetes Secrets are a type of Kubernetes object that stores sensitive data, such as:

+ Passwords
+ API keys
+ OAuth tokens
+ SSH keys
+ TLS certificates

Secrets are used to decouple sensitive data from the application code and configuration files. This provides several benefits:
+ **Security:** Sensitive data is not exposed in plain text.

+ **Flexibility:**  Secrets can be easily updated or rotated without modifying the application code.

+ **Portability:** Secrets can be used across multiple environments and clusters.

## Characteristics of Kubernetes Secrets:

+ **Base64 encoded:** Secrets are stored as Base64 encoded strings.

+ **Namespaced:** Secrets are scoped to a specific namespace.

+ **Access-controlled:** Access to Secrets is controlled using Kubernetes Role-Based Access Control (RBAC).

## Types of Kubernetes Secrets:

+ **Opaque Secrets:** General-purpose Secrets for storing arbitrary data.

+ **kubernetes.io/service-account-token:** Automatically generated Secrets for Service Accounts.

+ **kubernetes.io/dockercfg:** Secrets for storing Docker configuration.

+ **kubernetes.io/ssh-auth:** Secrets for storing SSH authentication data.

## Managing Kubernetes Secrets:

+ **Create:** Use the kubectl create secret command to create a new Secret.

+ **Update:** Use the kubectl patch secret command to update an existing Secret.

+ **Delete:** Use the kubectl delete secret command to delete a Secret.

+ **List:** Use the kubectl get secrets command to list all Secrets in a namespace.

Best practices for managing Kubernetes Secrets include:
+ **Use environment variables:** Instead of hardcoding sensitive data, use environment variables to reference Secrets.

+ **Use Secret management tools:** Consider using third-party tools, such as HashiCorp's Vault, to manage Secrets.

+ **Rotate Secrets regularly:** Regularly rotate Secrets to minimize the impact of a potential security breach.