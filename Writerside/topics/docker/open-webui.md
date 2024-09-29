**首先部署ollama
 - windows 
  ![image.png](https://pic-1255826935.cos.ap-guangzhou.myqcloud.com/20240924172546.png)
 - linux
  ```bash
  # ubunut 使用 snap 安装
  snap install ollama
  # 使用官方脚本安装
  curl -fsSL https://ollama.com/install.sh | sh
  ```

**运行 open-webui
  ```bash
  # **Nvidia GPU support** use this command to pull image
  docker pull ghcr.io/open-webui/open-webui:cuda
  
  # run the image
  docker run --detach \
  --name open-webui \
  --gpus all \
  --publish 3000:8080 \
  --add-host=host.docker.internal:host-gateway \
  --volume $HOME/.open-webui/data:/app/backend/data  \
  --restart always \
  ghcr.io/open-webui/open-webui:cuda

  # inline
  docker run --detach --name open-webui --publish 3000:8080 --gpus all --add-host=host.docker.internal:host-gateway --volume $HOME/.runtime/open-webui/data:/app/backend/data  --restart always ghcr.io/open-webui/open-webui:cuda
  ```
