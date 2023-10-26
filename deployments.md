Create a Service to Expose the Web Frontend Deployment's Pods Externally

```
k create svc nodeport web-frontend-svc --tcp=80:80 --node-port=30080 --dry-run=client -o yaml > svc.yaml
```

- manually update the selector 
- manually add the namespace 