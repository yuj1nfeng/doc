使用 `apt` 包管理器来安装 Docker。以下是具体步骤：

1. **添加 Docker 的官方 GPG 密钥**：
   ```bash
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmour -o /etc/apt/trusted.gpg.d/docker.gpg
   ```

2. **将 Docker 存储库添加到你的 APT 源中**：
   根据你使用的是 Ubuntu 的哪个版本来选择合适的存储库。这里以 Ubuntu 20.04 (Focal Fossa) 为例：

   ```bash
   sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
   ```

3. **更新包列表并安装 Docker**：
   ```bash
   sudo apt update
   sudo apt install docker-ce docker-ce-cli containerd.io
   ```

4. **验证安装**：
   ```bash
   sudo docker --version
   ```

  你应该会看到类似如下的输出，显示 Docker 的版本号。

5. **启用 Docker 服务（可选）**:

  你可以通过以下命令启动并设置 Docker 服务以在系统启动时自动运行：

  1. **启动 Docker**：
   ```bash
   sudo systemctl start docker
   ```

  2. **启用 Docker 在系统启动时自动运行**：
   ```bash
   sudo systemctl enable docker
   ```