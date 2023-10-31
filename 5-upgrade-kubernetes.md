# Upgrade kubeadm

```
sudo apt-get update 
sudo apt-get install -y --allow-change-held-packages kubeadm=1.27.2-00
```

# Drain node
```
kubectl drain acgk8s-control --ignore-daemonsets
```

# Plan the upgrade
```
sudo kubeadm upgrade plan v1.27.2
```

# apply upgrade 
```
sudo kubeadm upgrade apply v1.27.2
```

# Upgrade kubelet and kubectl
```
sudo apt-get update && \
sudo apt-get install -y --allow-change-held-packages kubelet=1.27.2-00 kubectl=1.27.2-00
```

# reload 
```
sudo systemctl daemon-reload
```

#  restart kubelet
```
sudo systemctl restart kubelet
```

# uncorden node 
```
kubectl uncordon acgk8s-control
```