-   项目地址: [ComfyUI](https://github.com/comfyanonymous/ComfyUI)
-   教程地址: [Comflowy](https://www.comflowy.com/zh-CN/docs)

**下载项目**

```bash
git clone git@github.com:comfyanonymous/ComfyUI.git
```

**下载依赖**

```bash
cd ComfyUI
pip install -r requirements.txt
pip install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/nightly/cu124
```

**确保 CUDA 和 PyTorch 已经正确安装并兼容**

-   检查

```bash
python -c "import torch; print(torch.__version__, torch.cuda.is_available())"
```

-   如果不兼容,先卸载 pytorch

```bash
pip uninstall torch
```

-   重新安装 pytorch

```bash
pip install --pre torch torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly/cu124
```

**启动**

```bash
python main.py
```

**中文插件**

-   地址 https://github.com/AIGODLIKE/AIGODLIKE-COMFYUI-TRANSLATION
-   进入 ComfyUI/custom_nodes

```bash
cd custom_nodes
git clone https://github.com/AIGODLIKE/AIGODLIKE-COMFYUI-TRANSLATION.git
```

-   重启应用
-   Settings > AGC > Locale
    
-   切换成功
    

**ComfyUI Manager**

-   地址 https://github.com/ltdrdata/ComfyUI-Manager.git
-   进入 ComfyUI/custom_nodes
-   安装方式同上

**模型位置配置**

-   参考 [下载 & 导入模型 – Comflowy](https://www.comflowy.com/zh-CN/preparation-for-study/model)
-   已安装过 SD WebUI
    -   修改 `extra_model_paths.yaml.example`
    -   `base_path: path/to/stable-diffusion-webui/`
    -   将文件重命名为 `extra_model_paths.yaml`
-   未安装过 SD WebUI
    -   模型文件都在项目 `models` 目录下
        
