# Deployments 

## 1. Edit the foo-frontend Deployment to Expose the HTTP Port

```
k edit deploy/foo-frontend -n foo
```

add a container port 
```
spec:
  containers:
  - image: nginx:1.14.2
    ports:
    - containerPort: 80

```

## 2. Create a Service to Expose the foo Deployment's Pods Externally
    Nodeport: 30080
    containerPort: 80

```
k create svc nodeport foo-svc --tcp=80:80 --node-port=30080 -n bar --dry-run=client -o yaml > svc.yaml
```

```
apiVersion: v1
kind: Service
metadata:
  creationTimestamp: null
  labels:
    app: foo-svc
  name: foo-svc
  namespace: bar
spec:
  ports:
  - name: 80-80
    nodePort: 30080
    port: 80
    protocol: TCP
    targetPort: 80
  selector:
    app: web-foo
  type: NodePort
status:
  loadBalancer: {}
```

- manually update the selector 

## 3. Create an Ingress That Maps to the New Service

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