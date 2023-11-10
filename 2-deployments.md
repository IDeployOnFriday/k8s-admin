# Deployments 

## 1. Create a Service to Expose the foo Deployment's Pods Externally
    Nodeport: 30080
    containerPort: 80

```
k create svc nodeport foo-svc --tcp=80:80 --node-port=30080 --dry-run=client -o yaml > svc.yaml
```

- manually update the selector 
- manually add the namespace 

## 2. Create an Ingress That Maps to the New Service

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: minimal-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  ingressClassName: nginx-example
  rules:
  - http:
      paths:
      - path: /testpath
        pathType: Prefix
        backend:
          service:
            name: test
            port:
              number: 80
```
Link to ingress template 
https://raw.githubusercontent.com/kubernetes/website/main/content/en/examples/service/networking/minimal-ingress.yaml