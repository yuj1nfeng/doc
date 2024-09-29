###### 更新系统包列表：

```bash
apt update
```

###### 安装必要的依赖：

```bash
apt install -y curl wget apt-transport-https
```

###### 安装 Docker（如果尚未安装）：

```bash
  apt install docker.io
  systemctl start docker
  systemctl enable docker
```

###### 下载并安装 Minikube：

```bash
wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
mv minikube-linux-amd64 /usr/local/bin/minikube
chmod +x /usr/local/bin/minikube
```

###### 安装 kubectl：

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

###### 启动 Minikube：

```bash
minikube start --driver=docker
```

###### 验证安装：

```bash
kubectl get nodes
minikube status
```

###### (可选）启用 Minikube 的 dashboard：

```bash
minikube dashboard
```

###### 注意事项：

-   确保您的系统有足够的资源（至少 2GB RAM 和 20GB 磁盘空间）。
-   如果遇到权限问题，可能需要将当前用户添加到 docker 组：

```bash
usermod -aG docker $USER && newgrp docker
```

-  如果在虚拟机中运行，确保启用了嵌套虚拟化。
