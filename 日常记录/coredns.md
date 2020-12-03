```
docker run -d \
  --restart always \
  --name coredns \
  -p 53:53/tcp \
  -p 53:53/udp \
  -v /opt/coredns/hosts:/etc/hosts \
  -v /opt/coredns/Corefile:/Corefile \
  192.168.80.54:8081/coredns/coredns:latest
```