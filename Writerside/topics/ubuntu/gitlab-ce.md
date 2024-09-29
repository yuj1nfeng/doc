###### 更新系统包列表：

```shell
apt update
apt upgrade-y
```

###### 安装必要的依赖：

```bash
apt install -y curl openssh-server ca-certificates tzdata perl apt-transport-https
```

###### 添加 GitLab 官方仓库：

```bash
 curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | bash
```

###### 安装 GitLab CE：

```bash
apt install gitlab-ce
```

###### 配置 GitLab：

-   安装完成后，打开 GitLab 配置文件：

```bash
vim /etc/gitlab/gitlab.rb
```

-   找到并修改 external_url 行，设置为你的域名或 IP 地址：

```.env
external_url 'http://your_domain_or_ip'
```

###### 重新配置 GitLab：

```bash
gitlab-ctl reconfigure
```

###### 获取初始密码

```bash
grep 'Password:' /etc/gitlab/initial_root_password
```

###### 访问 GitLab：

-   在浏览器中打开 http://your_domain_or_ip。

###### 登录：

-   使用用户名 root 和你刚刚获取的密码登录。

###### 卸载

```bash
gitlab-ctl stop
apt remove gitlab-ce
apt autoremove
rm -rf /opt/gitlab
rm -rf /var/opt/gitlab
rm -rf /etc/gitlab
```
