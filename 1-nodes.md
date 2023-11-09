# 1 -  working with nodes

## Count the number of nodes that are ready to run normal workloads

```
   k get nodes --no-headers | grep -v -c control-plane > count.txt
```

## Retrieve Error Messages from the Container foo in pod bar, in the foobar namespace 
```
k logs bar -c foo -n foobar | grep ERROR > /k8s/0002/errors.txt
```
  
## Find the Pod with a Label of app=foo in the foobar Namespace That Is Utilizing the Most CPU

```
k top pods -n foobar --selector='app=foo' 

echo foo-web > /k8s/0003/cpu-pod.txt 

```
