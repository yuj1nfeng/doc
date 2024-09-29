## 安装
### 使用 `apt` 包管理器来安装 Docker。以下是具体步骤：
- 添加 Docker 的官方 GPG 密钥
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmour -o /etc/apt/trusted.gpg.d/docker.gpg
```

- 将 Docker 存储库添加到你的 APT 源中  
  _根据你使用的是 Ubuntu 的哪个版本来选择合适的存储库。这里以 Ubuntu 20.04 (Focal Fossa) 为例：_

```bash
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

- 更新包列表并安装 Docker
```bash
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
```
### 使用 `snap` 包管理器来安装 Docker。以下是具体步骤：
```bash
sudo snap install docker
```

### 配置Docker
安装完成后，Docker可能需要一些额外的配置才能正常运行
首先，确保你的用户属于docker组，这样你就可以无sudo执行Docker命令
```bash
sudo usermod -aG docker $USER
```

### 验证安装
```bash
sudo docker --version
```
_你应该会看到类似如下的输出，显示 Docker 的版本号_
```bash
(base) root@ubuntu:~# docker --version
Docker version 27.3.1, build ce12230
```
### 启用 Docker 服务  
_你可以通过以下命令启动并设置 Docker 服务以在系统启动时自动运行_
```bash
sudo systemctl start docker
sudo systemctl enable docker
```

## `Dockerfile` 模板
### nodejs
```Dockerfile
FROM node:latest
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN mkdir -p /app
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 80
CMD ["npm","run","start"]
```
### goang
```Dockerfile
# 使用官方的Golang基础镜像作为父镜像
FROM golang:alpine AS builder

# 设置工作目录
WORKDIR /app

# 将当前目录下的所有文件复制到容器的/app目录下
COPY . .

# 使用go mod下载依赖（如果你的项目使用go modules）
RUN go mod download

# 编译你的Go应用
RUN GOOS=linux GOARCH=amd64 go build -o main .

# 使用另一个更小的基础镜像作为最终运行时镜像
FROM alpine:latest

# 设置工作目录
WORKDIR /app

# 将上一阶段编译生成的可执行文件从builder镜像复制过来
COPY --from=builder /app/main /app/

# 运行你的应用
CMD ["/app/main"]
```
### python
```Dockerfile
# 使用官方的Python基础镜像，可以选择指定版本，比如3.8、3.9等
FROM python:3.7-slim-buster

# 设置工作目录
WORKDIR /usr/src/app

# 设置环境变量，可选，用于安装pip包时指定国内镜像源加速下载
# ENV PIP_CONFIG_FILE=/root/.pip/pip.conf

# 安装任何需要的系统包，比如编译一些Python包所需的库
# RUN apt-get update && apt-get install -y --no-install-recommends \
#      build-essential \
#      libssl-dev \
#      && rm -rf /var/lib/apt/lists/*

# 将当前目录下的requirements.txt复制到容器中
COPY requirements.txt .

# 安装项目所需的所有Python依赖
RUN pip install --no-cache-dir -r requirements.txt

# 将项目的所有文件复制到容器中（确保requirements.txt之后复制，以利用缓存）
COPY . .

# 设定容器启动时运行的命令，比如你的主脚本文件
CMD ["python", "./your_app.py"]
```
### java
```Dockerfile
# 使用官方的Java运行时作为基础镜像，这里以Java 11为例
FROM adoptium/openjdk11:jdk-11.0.13_8-alpine

# 设置工作目录
WORKDIR /app

# 将本地的Maven构建好的jar包复制到容器中，这里假设构建产物名为app.jar
COPY target/my-java-app.jar /app/app.jar

# 声明运行时环境变量，例如配置Spring Boot应用的profile
ENV SPRING_PROFILE=prod

# 暴露容器需要监听的端口
EXPOSE 8080

# 定义容器启动时执行的命令，使用Java命令运行jar包
CMD ["java","-jar","-Dspring.profiles.active=${SPRING_PROFILE}","app.jar"]
```
### nginx
```Dockerfile
# 使用官方的 Nginx 镜像作为基础镜像
FROM nginx:stable-alpine

# 将本地的配置文件复制到容器中的 Nginx 配置目录
COPY nginx.conf /etc/nginx/nginx.conf

# 将静态资源从本地复制到容器的指定目录（如果有的话）
COPY static_files /usr/share/nginx/html

# 可选：如果需要修改或添加 SSL 证书
# COPY cert.crt /etc/nginx/certs/cert.crt
# COPY cert.key /etc/nginx/certs/cert.key

# 可选：开启 SSL 支持并配置证书路径
# RUN sed -i 's/# server {/server {\
#         listen 80 default_server;\n\
#         listen [::]:80 default_server;\n\
#         server_name _;\n\
#         return 301 https://$host$request_uri;/g' /etc/nginx/conf.d/default.conf
# RUN sed -i '/listen 443 ssl;/a \    ssl_certificate /etc/nginx/certs/cert.crt;\n    ssl_certificate_key /etc/nginx/certs/cert.key;' /etc/nginx/conf.d/default.conf

# 曝光端口
EXPOSE 80
# 如果启用了SSL，还需暴露443端口
# EXPOSE 443

# 定义容器启动时执行的命令，默认Nginx已经包含启动命令
CMD ["nginx", "-g", "daemon off;"]
```