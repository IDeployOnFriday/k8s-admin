Create a Multi-Container Pod

```
k run multi --image=nginx -n baz -o yaml --dry-run=client > multipod.yaml
```
- edit yaml to add in extra container 
```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: multi
  name: multi
  namespace: baz
spec:
  containers:
  - name: nginx-container
    image: nginx
  - name: redis-container
    image: redis
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```

