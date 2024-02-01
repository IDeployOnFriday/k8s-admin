# A node is broken, determine which node and what is wrong 

```
k get nodes 
```

# determine what is wrong 

```
kubectl describe node acgk8s-broken-worker2
```

# fix broken node 

## ssh onto the node 

## check the kubelet status
```
systemctl status kubelet 
```

## enable and start kubelet
```
sudo systemctl enable kubelet
sudo systemctl start  kubelet
```

## verify kubelet is status
```
systemctl status kubelet 
```
# exit 
# check all nodes are now in a ready state  