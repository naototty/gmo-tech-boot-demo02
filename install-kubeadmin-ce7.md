# install kubernetes 1.6 on centos 7.3

## Install kubelet, kubeadm, docker, kubectl and kubernetes-cni

### 1. Install Yum Repo
```
cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=http://yum.kubernetes.io/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg
        https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
EOF
```

### 2. Disable SELinux

```
setenforce 0
```

### 3. Install from yum

```
yum install -y docker kubelet kubeadm kubectl kubernetes-cni
```

### 4. Enable docker and kubelet

```
systemctl enable docker && systemctl start docker
systemctl enable kubelet && systemctl start kubelet
```

### 5. Edit the 10-kubadm.conf [see](https://github.com/kubernetes/kubernetes/issues/43805)

```
vi /etc/systemd/system/kubelet.service.d/10-kubeadm.conf
```

Add the following before "ExeStart="

```
Environment="KUBELET_EXTRA_ARGS=--cgroup-driver=systemd"
```

### 6. Enable Overlay FS

```
sudo tee /etc/modules-load.d/overlay.conf <<-'EOF'
overlay
EOF
```

### 7. Reboot to reload kernel modules

```
reboot
```

### 8. Verify that OverlayFS is enabled:

```
lsmod | grep overlay
overlay
```

### 9. Edit the docker-storage-setup file

```
vi /etc/sysconfig/docker-storage-setup
```

add 

```
STORAGE_DRIVER="overlay"
```

### 10. Start Docker and Kubelet Services

```
systemctl start docker
systemctl start kubelet
```