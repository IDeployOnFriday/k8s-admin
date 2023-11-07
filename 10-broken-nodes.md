# A node is broken, determine which node and what is wrong 

```
k get nodes 
```

# determine what is wrong 

```
kubectl describe node acgk8s-broken-worker2
```

# fix broken node 
1. ssh onto the node 
2. check the kubelet log 
3. check the kubelet status
4. enable kubelet
5. start kubelet 
6. verify kubelet is status
7. exit 
8. check all nodes are now in a ready state  