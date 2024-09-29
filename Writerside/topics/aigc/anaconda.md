

## 下载
- [linux](https://repo.anaconda.com/archive/Anaconda3-2024.06-1-Linux-x86_64.sh)
- [windows](https://repo.anaconda.com/archive/Anaconda3-2024.06-1-Windows-x86_64.exe)
- [mac(apple silicon) command line install](https://repo.anaconda.com/archive/Anaconda3-2024.06-1-MacOSX-arm64.sh)
## 安装
一路next....

## 使用
- 环境列表
```bash
conda env list
```
```bash
(base) PS C:\Users\Administrator> conda env list
# conda environments:
#
base                  *  C:\ProgramData\anaconda
sd                       C:\ProgramData\anaconda\envs\sd
```
- 创建虚拟环境
```bash
conda create --name env_name python=python_version
```
- 激活虚拟环境
```bash
conda activate env_name
```
- 删除虚拟环境
```bash
conda remove -n env_name --all
```