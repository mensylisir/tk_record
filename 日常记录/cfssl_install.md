## sfssl 安装 ##

### 安装golang

要求golang版本大于等于1.12

#### ubuntu
```
sudo apt install golang
```

#### centos
```
sudo dnf install golang
```

### 编译cfssl
``````
git clone https://github.com/cloudflare/cfssl.git 
cd cfssl
make
``````

### 目录树如下
```
$ tree bin
bin
├── cfssl
├── cfssl-bundle
├── cfssl-certinfo
├── cfssl-newkey
├── cfssl-scan
├── cfssljson
├── mkbundle
└── multirootca

0 directories, 8 files
```
