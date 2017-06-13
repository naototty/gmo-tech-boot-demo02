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


### 1-1) CentOS 7の場合

https://docs.docker.com/engine/installation/linux/centos/#install-docker


古いdockerに関係するパッケージをun-installします

``` bash
$ sudo yum remove docker \
                  docker-common \
                  container-selinux \
                  docker-selinux \
                  docker-engine
```

dockerの環境を手動で構築してみます
dockerに必要なパッケージをインストールします


``` bash
  sudo yum install -y yum-utils device-mapper-persistent-data lvm2
  
```

dockerの公式から、docker-ce (community edition)を取得するためのリポジトリを設定します

``` bash
$ sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo  
```

docker-ce-edge をenableにします

``` bash
$ sudo yum-config-manager --enable docker-ce-edge

```

docker-ce をインストールします

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


### 事前準備・構築: docker環境を作る)



dockerのサービスが起動しているのか確認します。起動していないのがわかります

``` bash
# systemctl status docker
● docker.service - Docker Application Container Engine
   Loaded: loaded (/usr/lib/systemd/system/docker.service; disabled; vendor preset: disabled)
   Active: inactive (dead)
     Docs: https://docs.docker.com
```


dockerのサービスを起動します

``` bash
systemctl start docker
```

これで、dockerがつかえるようになります



### 確認: dockerの動作)

a) hello-world コマンドラインdockerアプリケーションの実行

``` bash
# docker run hello-world
```


b) cowsayという牛がなんか喋っているふうの絵が出るコマンドラインdockerアプリケーションの実行

``` bash
# docker run docker/whalesay cowsay
```

c) qiitaにある「練習.4」以降もやってみよう


## 3) make hands on "docker01"; docker-machine

Docker MachineでCentOS7をプロビジョンする方法
http://qiita.com/zembutsu/items/04f896a96d0fc857f3a7

- 記事では、CentOS 7.2をDigital Ocean上に起動する方法についてに記載されているが、ConoHaではどうするのかやってみる
- docker-machine でdockerの環境を作って、dockerでアプリケーションを利用しよう


### 課題)
"docker-machine"でUbuntu 16.04を2GB memoryでプロビジョニングする


### 事前準備)
- Pythonのvirtualenvを使ったopenstack clientのインストールと動作環境の構築が終わっている
- osrc_* 環境設定ファイルの作成と適用ができている
- "my-local-key" のkey-pairの登録、ローカルのPrivate keyとして ~/.ssh/id_rsa が存在する(ssh-keygen実行による)
- docker-machineのインストール

以下、一行です
```bash
# curl -L https://github.com/docker/machine/releases/download/v0.10.0/docker-machine-`uname -s`-`uname -m` >/tmp/docker-machine && \
  chmod +x /tmp/docker-machine && \
  cp /tmp/docker-machine /usr/local/bin/docker-machine
```


### 作成方法)
先程の
"osrc*"
でのOpenStack環境設定を利用します

docker-machine コマンドは、OpenStackのクラウドを利用するユーザ情報を環境変数から読み込みすることで、ユーザ依存の情報を別に管理して運用することが出来ます。


SSH public keyの登録が必要
>> コンパネでやる

下記の "my-local-key" は自分で登録したssh key-pairの名前

``` bash
openstack keypair list
```


flavor-name は次のコマンドで一覧を取得して、その中から2GBの物を選択

``` bash
openstack flavor list
```


image-name は次のコマンドで一覧を取得して、その中からUbuntu 16.04 amd64を選択

``` bash
openstack image list -f csv
```


sec-groups (セキュリティ・グループ)は、一度コントロールパネルでvmを作成した場合、"default,gncs-ipv4-all" という「すべての通信を許可する」ルールがコントロールパネルにより作成されるので、これを利用する。


``` bash
docker-machine create \
  -d openstack \
  --openstack-flavor-name g-2gb \
  --openstack-image-name vmi-ubuntu-16.04-amd64-unified \
  --openstack-keypair-name my-local-key \
  --openstack-private-key-file ~/.ssh/id_rsa \
  --openstack-ssh-user root \
  --openstack-sec-groups "default,gncs-ipv4-all" \
  test

```

実行すると、vmが作成され、dockerの環境を構築する(dockerのインストールなど)
dockerのインストールをして、ユーザが利用できる状態にすることを「プロビジョニング」という


### プロビジョニングの確認)

先程のdocker演習で実行したコマンドラインdockerアプリケーションを実行してみましょう

``` bash
# docker-machine ssh test

(remoteの作成したvmにlogin)

# docker ps

# docker run docker/whalesay cowsay
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
