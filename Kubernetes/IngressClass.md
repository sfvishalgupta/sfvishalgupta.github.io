#### [Back](./Kubernetes-Resources.md)

# K8 IngressClass

An IngressClass is a Kubernetes resource that defines a class of Ingresses that can be implemented by one or more Ingress controllers. IngressClasses provide a way to define a set of parameters and annotations that can be used to customize the behavior of an Ingress controller.

## Characteristics of IngressClass

+ **Parameters and annotations:** IngressClasses define a set of parameters and annotations that can be used to customize the behavior of an Ingress controller.

+ **Ingress controller selection:** IngressClasses provide a way to select the Ingress controller that will implement the Ingress.

+ **Customization:** IngressClasses provide a way to customize the behavior of an Ingress controller.

```yaml
apiVersion: networking.k8s.io/v1
kind: IngressClass
metadata:
  name: external-lb
spec:
  controller: external-lb.k8s.io/external-lb
  parameters:
    apiGroup: external-lb.k8s.io
    kind: ExternalLBParameters
    name: external-lb-params
```

```bash
kubectl apply -f external-lb-ingressclass.yaml
```