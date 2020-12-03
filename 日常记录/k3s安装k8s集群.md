> 1. 将tar包放置在/var/lib/rancher/k3s/agent/images/
>
>    ```
>    cp k3s-airgap-images-amd64.tar /var/lib/rancher/k3s/agent/images
>    ctr image ls
>    ```

> 2. 将k3s放置在/usr/loca/bin
>
>    ```
>    cp k3s /usr/local/bin
>    ```

> 3. 启动server
>
>    ```
>    k3s server &
>    ```

> 4. 加入node
>
>    ```shell
>    k3s agent --server https://192.168.80.86:6443 --token K101ec81fb691b95f0f03c95cf74848d19a029d1feb9341f0d142e83078401fab19::server:5fe4e267681a562a2c711c4f1fc39794
>    ```

> 5. 查看NODE_TOKEN
>
>    ```
>    cat /var/lib/rancher/k3s/server/node-token
>    ```

> 6. 杀死containerd
>
>    ```
>    kill -9 `ps -ef | grep contain* | awk '{print $2}'`
>    ```

> 7. 安装docker
>
>    ```
>    scp -P7122 root@192.168.80.76:/usr/bin/docker* /usr/bin/
>    ```
>
>    ```
>    scp -P7122 root@192.168.80.76:/usr/lib/systemd/system/docker.service /usr/lib/systemd/system/docker.service
>    
>    systemctl daemon-reload
>    systemctl start docker
>    systemctl status docker
>    ```

> 8. 导入k3s镜像
>
>    ```
>    docker load < k3s-airgap-images-amd64.tar
>    ```

> 9. 复制k3s到/usr/loca/bin
>
>    ```
>    mv k3s /usr/local/bin
>    ```
>
>    ```
>    chmod +x install.sh
>    ```
>
>    ```
>    chmod +x /usr/local/bin/k3s
>    ```

> 10. 部署k3s server
>
>     ```
>     export INSTALL_K3S_SKIP_DOWNLOAD=true     //设置跳过下载k3s二进制文件
>     ```
>
>     ```
>     export INSTALL_K3S_BIN_DIR=/usr/local/bin       //设置k3s安装目录
>     export INSTALL_K3S_EXEC="server --docker --no-deploy traefik --cluster-init"
> # 如果是多server
>     export INSTALL_K3S_EXEC="server --docker --no-deploy traefik --server https://myserver:6443"
>     ```
>     
>     ```
>     bash install.sh
>     ```

> 11. 修改配置
>
>     ```
>     nano /etc/systemd/system/k3s.service
>     ```
>
>     ```
>     ExecStart=/usr/local/bin/k3s server --pause-image=192.168.80.54:8081/rancher/pause-amd64:3.1
>     ```

> 12. agent
>
>     ```
>     export INSTALL_K3S_SKIP_DOWNLOAD=true     //设置跳过下载k3s二进制文件
>     export INSTALL_K3S_BIN_DIR=/usr/local/bin
>     export INSTALL_K3S_EXEC="server --docker --no-deploy traefik"
>     export K3S_URL=https://192.168.80.82:6443
>     export K3S_TOKEN=K10de0ee6b8b5fd2e4312ba1c6ca1493e17d4d0e886cc53c4751c689dd04ef83f3a::server:b66e9a18219eade075b2414f26c910db
>     ```
>
>     ```
>     bash install.sh
>     ```



```
scp -P7122 root@192.168.80.86:/opt/k8s/k3s-airgap-images-amd64.tar /opt/k8s/
scp -P7122 root@192.168.80.86:/opt/k8s/k3s /opt/k8s/
scp -P7122 root@192.168.80.86:/opt/k8s/install.sh /opt/k8s/
```

```
scp -P7122 root@192.168.80.76:/usr/bin/docker* /usr/bin
scp -P7122 root@192.168.80.76:/usr/lib/systemd/system/docker.service /usr/lib/systemd/system/docker.service
```

```
nano /etc/systemd/system/multi-user.target.wants/k3s.service
/usr/local/bin/k3s server --docker --no-deploy traefik
systemctl daemon-reload
service k3s restart
```

```

```