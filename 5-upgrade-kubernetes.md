# Upgrade All Kubernetes Components on the Control Plane Node

## Upgrade kubeadm

```
sudo apt-mark unhold kubeadm && 
sudo apt-get update 
sudo apt-get install -y kubeadm='1.27.2-00' 
sudo apt-mark hold kubeadm
```

## verify download 
```
kubeadm version
```

## PVerify the upgrade plan
```
sudo kubeadm upgrade plan 
```

## Choose a version to upgrade
```
sudo kubeadm upgrade apply v1.27.2
```

# Upgrade kubelet and kubectl
```
sudo apt-mark unhold kubelet kubectl 
sudo apt-get update
sudo apt-get install -y kubelet='1.27.2-00' kubectl='1.27.2-00' 
sudo apt-mark hold kubelet kubectl
```

##  restart kubelet
```
sudo systemctl daemon-reload
sudo systemctl restart kubelet
```


# Upgrade All Kubernetes Components on the Worker Nodes

## ssh onto worker node
```
ssh acgk8s-worker1
```

## Drain worker node
```
sudo apt-mark unhold kubeadm 
sudo apt-get update 
sudo apt-get install -y kubeadm='1.27.2-00' 
sudo apt-mark hold kubeadm
```

## upgrade node
```
sudo kubeadm upgrade node
```

## drain node 

```
exit 
kubectl drain <node-to-drain> --ignore-daemonsets
```


## upgrade kubectl and kubeadm
```
sudo apt-mark unhold kubelet kubectl 
sudo apt-get update 
sudo apt-get install -y kubelet='1.27.2-00' kubectl='1.27.2-00' 
sudo apt-mark hold kubelet kubectl
``` 

## Restart the kubelet 
```
sudo systemctl daemon-reload
sudo systemctl restart kubelet
```

## uncorden worker node 
```
exit 
kubectl uncordon acgk8s-worker1
```

## repeat for other worker node 