# gmo-tech-boot-demo02
gmo tech boot camp docker01 (Docker)

This repo is gmo boot camp docker01.
https://github.com/naototty/gmo-tech-boot-demo02

まずは、ConoHa上で作業
なんやねん、Dockerって

## 1) quick start docker env. on ConoHa cloud
https://docs.docker.com/engine/docker-overview/


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

## 2) make Hands on "docker01" work dir

