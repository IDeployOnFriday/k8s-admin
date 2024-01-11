## Add the following from the 7A 

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: localdisk
provisioner: kubernetes.io/no-provisioner
allowVolumeExpansion: true
```

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

## 7B question, create pod to use pvc 
https://raw.githubusercontent.com/kubernetes/website/main/content/en/examples/pods/storage/pv-pod.yaml

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: host-storage-pvc
  namespace: auth
spec:
  storageClassName: localdisk
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 100Mi
```


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