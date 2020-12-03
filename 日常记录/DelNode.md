```shell
systemctl stop kubelet

systemctl stop kube-proxy

systemctl stop docker

systemctl stop flanneld

rm -rf /usr/bin/docker*

rm -rf /opt/*

rm -rf /usr/lib/systemd/system/docker.service /usr/lib/systemd/system/kubelet.service /usr/lib/systemd/system/kube-proxy.service /usr/lib/systemd/system/flanneld.service
```

```

```

