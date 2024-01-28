## backup etcd 

1. go to docs 
https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/#scaling-out-etcd-clusters
```
ETCDCTL_API=3 etcdctl --endpoints=https://127.0.0.1:2379 \
  --cacert=<trusted-ca-file> --cert=<cert-file> --key=<key-file> \
  snapshot save <backup-file-location>
```


2. copy commands into note pad 

3. populate commands 
```
ETCDCTL_API=3 etcdctl --endpoints=https://etcd1:2379  --cacert=/home/cloud_user/etcd-certs/etcd-ca.pem --cert=/home/cloud_user/etcd-certs/etcd-server.crt --key=/home/cloud_user/etcd-certs/etcd-server.key snapshot save /home/cloud_user/etcd_backup.db
```

## Restore from etcd 

1. stop etcd 
2. delete etcd data 
3. restore etcd from backup
4. set data ownership 
5. start etcd 

6. verify 

Example 

1. stop etcd 
```
sudo systemctl stop etcd
```
2. delete etcd data 
```
sudo rm -rf /var/lib/etcd
```
3. restore etcd from backup
```
sudo ETCDCTL_API=3 etcdctl snapshot restore /home/cloud_user/etcd_backup.db \
--data-dir /var/lib/etcd
```
4. set data ownership 
```
sudo chown -R etcd:etcd /var/lib/etcd
```
5. start etcd 
```
sudo systemctl start etcd
```
6. verify 
```
ETCDCTL_API=3 etcdctl get cluster.name \
--endpoints=https://etcd1:2379 \
```