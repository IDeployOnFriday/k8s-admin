# drain worker node 
```
k drain --ignore-daemonsets acgk8s-worker1
```
use flags provided when it fails 
link to docs - https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/


# label node 

```
k label node/acgk8s-worker2 bar=foo
k get nodes --show-labels
```


# Create a Pod That Will Only Be Scheduled on Nodes with a Specific Label

# create pod 
```
k run foo-nginx --image=nginx -n dev --dry-run=client -o yaml > foopod.yaml
```

# add nodeselector line to pod 

```
apiVersion: v1
kind: Pod
metadata:
  name: fast-nginx
  namespace: dev
spec:
  nodeSelector:
    bar: foo
  containers:
  - name: nginx
    image: nginx
```

# create pod 

```
k apply -f foopod.yaml 
```

check status of pod 
```
k get pod foo-nginx -n dev -o wide
```