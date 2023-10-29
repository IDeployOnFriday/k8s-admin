## backup etcd 

1. go to docs 
https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/#scaling-out-etcd-clusters
```
ETCDCTL_API=3 etcdctl --endpoints=https://127.0.0.1:2379 \
  --cacert=<trusted-ca-file> --cert=<cert-file> --key=<key-file> \
  snapshot save <backup-file-location>
```


2. copy commands into note pad 

3. popilate commands 
```
ETCDCTL_API=3 etcdctl --endpoints=https://etcd1:2379  --cacert=/home/cloud_user/etcd-certs/etcd-ca.pem --cert=/home/cloud_user/etcd-certs/etcd-server.crt --key=/home/cloud_user/etcd-certs/etcd-server.key snapshot save /home/cloud_user/etcd_backup.db
```

## Restore from etc d 