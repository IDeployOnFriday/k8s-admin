# create a PersistentVolume with 
1G storage 
HostPath /etc/data 
reclaimPolicy recyle 

# steps 

1. create storage class using docs 
2. create pv using docs 
3. apply 

example storage class 
```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: localdisk
provisioner: kubernetes.io/no-provisioner
allowVolumeExpansion: true
```

example pv
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

# create a pod to use the pv

## create pvc 
https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: task-pv-claim
spec:
  storageClassName: manual
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 3Gi
```

## create pod to use pvc 
https://raw.githubusercontent.com/kubernetes/website/main/content/en/examples/pods/storage/pv-pod.yaml

```
apiVersion: v1
kind: Pod
metadata:
  name: task-pv-pod
spec:
  volumes:
    - name: task-pv-storage
      persistentVolumeClaim:
        claimName: task-pv-claim
  containers:
    - name: task-pv-container
      image: nginx
      ports:
        - containerPort: 80
          name: "http-server"
      volumeMounts:
        - mountPath: "/usr/share/nginx/html"
          name: task-pv-storage
```