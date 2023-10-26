1. Create a Service to Expose the foo Deployment's Pods Externally
    Nodeport: 30080
    containerPort: 80

```
k create svc nodeport foo-svc --tcp=80:80 --node-port=30080 --dry-run=client -o yaml > svc.yaml
```

- manually update the selector 
- manually add the namespace 