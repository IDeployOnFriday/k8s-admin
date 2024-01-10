# create a PersistentVolume with 
1G storage 
HostPath /etc/data 
reclaimPolicy recyle 

# steps 

1. create storage class using docs 
    link local - https://kubernetes.io/docs/concepts/storage/storage-classes/
2. create pv using docs 
3. apply 

example storage class 
```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: llocal-storage
provisioner: kubernetes.io/no-provisioner
allowVolumeExpansion: true
```

example pv
link - https://raw.githubusercontent.com/kubernetes/website/main/content/en/examples/pods/storage/pv-volume.yaml
```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: host-storage-pv
spec:
  capacity:
    storage: 1Gi
  storageClassName: localdisk
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Recycle
  hostPath:
    path: /etc/data
```