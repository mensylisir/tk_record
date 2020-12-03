## etcd集群

  [Kubernetes二进制部署——单master集群部署（1）-一拳超人-51CTO博客](https://blog.51cto.com/14080162/2469960)

[k8s学习笔记-部署ETCD3.4集群_snipercai的博客-CSDN博客](https://blog.csdn.net/snipercai/article/details/101012124)



1. vim /opt/etcd/cfg/etcd

```
#[Member]
ETCD_NAME="etcd01"
ETCD_DATA_DIR="/var/lib/etcd/default.etcd"
ETCD_LISTEN_PEER_URLS="https://192.168.80.76:2380"
ETCD_LISTEN_CLIENT_URLS="https://192.168.80.76:2379"

#[Clustering]
ETCD_INITIAL_ADVERTISE_PEER_URLS="https://192.168.80.76:2380"
ETCD_ADVERTISE_CLIENT_URLS="https://192.168.80.76:2379"
ETCD_INITIAL_CLUSTER="etcd01=https://192.168.80.76:2380,etcd02=https://192.168.80.77:2380,etcd03=https://192.168.80.78:2380"
ETCD_INITIAL_CLUSTER_TOKEN="etcd-cluster"
ETCD_INITIAL_CLUSTER_STATE="new"
ETCD_ENABLE_V2="true"
```

2. vim /lib/systemd/system/etcd.service

   ```
   [root@DDBC-Master04 bin]# cat /lib/systemd/system/etcd.service                                                               
   [Unit]
   Description=Etcd Server
   After=network.target
   After=network-online.target
   Wants=network-online.target
   
   [Service]
   Type=notify
   EnvironmentFile=/opt/etcd/cfg/etcd
   ExecStart=/opt/etcd/bin/etcd \
   --cert-file=/opt/etcd/ssl/server.pem \
   --key-file=/opt/etcd/ssl/server-key.pem \
   --peer-cert-file=/opt/etcd/ssl/server.pem \
   --peer-key-file=/opt/etcd/ssl/server-key.pem \
   --trusted-ca-file=/opt/etcd/ssl/ca.pem \
   --peer-trusted-ca-file=/opt/etcd/ssl/ca.pem
   Restart=on-failure
   LimitNOFILE=65536
   
   [Install]
   WantedBy=multi-user.target
   ```

   