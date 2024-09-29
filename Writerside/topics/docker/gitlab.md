**安装
```bash
docker run --detach `
--name gitlab `
--restart always `
--publish 80:80 `
--publish 443:443 `
--publish 22:22 `
--volume $HOME/.gitlab/config:/etc/gitlab `
--volume $HOME/.gitlab/logs:/var/log/gitlab `
--volume $HOME/.gitlab/data:/var/opt/gitlab `
gitlab/gitlab-ce
```
**获取初始密码
```bash
docker exec -it gitlab grep 'Password:' /etc/gitlab/initial_root_password
```
**修改配置文件
- /etc/gitlab/gitlab.rb
```.env
external_url "http://[your.host]" 
gitlab_rails['gitlab_ssh_host'] = '[your.host]' 
gitlab_rails['gitlab_shell_ssh_port'] = 22
```
**重新加载配置文件
```bash
docker exec -it gitlab gitlab-ctl reconfigure
```
