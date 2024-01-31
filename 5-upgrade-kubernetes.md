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


## Drain worker node
```
kubectl drain acgk8s-worker1 --ignore-daemonsets --force
```

## ssh onto worker node
```
ssh acgk8s-worker1
```

## install new version of kubeadm

```
sudo apt-get update && \
sudo apt-get install -y --allow-change-held-packages kubeadm=1.27.2-00
```
## upgrade node 

```
sudo kubeaddm upgrade node
```

## upgrade kubectl and kubeadm
```
sudo apt-get update && \
sudo apt-get install -y --allow-change-held-packages kubelet=1.27.2-00 kubectl=1.27.2-00
``` 

## reload 
```
sudo systemctl daemon-reload
```

## resart kubelet 
```
sudo systemctl restart kubelet
```

## exit node 
```
exit 
```

## uncorden worker node 
```
kubectl uncordon acgk8s-worker1
```
