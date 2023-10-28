

## Create a service account in the bar namespace called foo.
```
k create sa fooautomation -n bar
```

## Create a ClusterRole called pod-reader that has get, watch, and list access to all Pods
```
kubectl create clusterrole pod-reader --verb=get,list,watch --resource=pods
```

## Bind the ClusterRole to the webautomation service account so that it can read all Pods, but only in the web namespace.
```
kubectl create rolebinding rb-pod-reader --clusterrole=pod-reader --serviceaccount=bar:fooautomation -n bar
```