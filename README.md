# gmo-tech-boot-demo02
gmo tech boot camp docker01 (Docker)

This repo is gmo boot camp docker01.
https://github.com/naototty/gmo-tech-boot-demo02

まずは、ConoHa上で作業
なんやねん、Dockerって

1コンテナ : 1アプリケーション
というDockerコンテナが基本です。

Unixの概念の
1コマンド : 1機能
という概念に近いことを覚えておいてね。


## 1) quick start docker env. on ConoHa cloud
https://docs.docker.com/engine/docker-overview/

### 1-1) CentOS 7の場合 (今回はとばしてね)

https://docs.docker.com/engine/installation/linux/centos/#install-docker

``` bash
$ sudo yum remove docker \
                  docker-common \
                  container-selinux \
                  docker-selinux \
                  docker-engine
```

``` bash
  sudo yum install -y yum-utils device-mapper-persistent-data lvm2
  
```

``` bash
$ sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo  
```

``` bash
$ sudo yum-config-manager --enable docker-ce-edge

```

``` bash
$ sudo yum install docker-ce
```

### 1-2) Ubuntu 16.04の場合 << こちら

``` bash
$ sudo apt-get remove docker docker-engine
```

``` bash
$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
```

``` bash
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

``` bash
$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```


``` bash
$ sudo apt-get update
```

``` bash
$ sudo apt-get install docker-ce
```



## 2) make Hands on "docker01"; docker基本操作

Qiitaのつぎのページを開いて演習します(docker基本操作)
http://qiita.com/zembutsu/items/d146295cfcf69c205c1e

## 3) make hands on "docker01"; docker-machine

Docker MachineでCentOS7をプロビジョンする方法
http://qiita.com/zembutsu/items/04f896a96d0fc857f3a7

課題)
"docker-machine"でUbuntu 16.04をプロビジョニングする

先程の
"osrc_*"
でのOpenStack環境設定を利用します

SSH public keyの登録が必要
>> コンパネでやる

下記の"mykeypair"は自分で登録したkeyの名前

``` bash
docker-machine create \
  -d openstack \
  --openstack-flavor-name g-2gb \
  --openstack-image-name vmi-ubuntu-16.04-amd64-unified \
  --openstack-keypair-name mykeypair \
  --openstack-ssh-user root \
  --openstack-sec-groups "default,gncs-ipv4-all" \
  test
```


## 4) make Hands on "docker01"; docker compose(1)

Docker応用チュートリアル：WordPress
http://qiita.com/zembutsu/items/26cb3a3d138d26c42bab

``` bash
docker-machine ssh test
```
ssh loginします

## 5) make Hands on "docker01"; docker compose(2)

Rocket.ChatをDocker Composeで使う
http://qiita.com/zembutsu/items/eea5c3216911b1ee71e1

以下のコマンドでファイルを作ります

``` bash

cat > docker-compose.yml < __EOF_
rocketchat:
  image: rocketchat/rocket.chat
  environment:
    - MONGO_URL=mongodb://mongodb/rocketchat
    - ROOT_URL=http://localhost:80
  links:
    - mongodb
  ports:
    - 80:80

mongodb:
   image: mongo
   ports:
     - 27017

__EOF_
```

## 5) make Hands on "docker01"; Rancher / Kubernetes

Rancher/Kubernetes入門ハンズオン
http://qiita.com/zembutsu/items/007617cbb00a0d554c8c

さくらのクラウド ==> ConoHa cloud
に読み替えてやってみよう

Rancherの設定までできたらOK


## 6) スーパー応用編

ここまで出来たら、一人前じゃね
足りない情報は、自分でリサーチして補完して、次の構築が出来たら、ConoHaエンジニアリング・チームにスカウトしちゃいます
(ほんとに、スカウトできるかはわからないけど、ConoHaグッズぐらいプレゼントできるかな)

以下、"オイラ"の仕事 みたいなもの

Kolla-kubernetes
https://docs.openstack.org/developer/kolla-kubernetes/deployment-guide.html

helmでkubernetes上にOpenStackインストール
https://github.com/openstack/openstack-helm
