**下载 COLMAP**
- 你可以从 COLMAP 的 GitHub 页面下载 Windows 版本的预编译二进制文件。
- 下载链接 [colmap (github.com)](https://github.com/colmap/colmap/releases)
  ![image.png](https://pic-1255826935.cos.ap-guangzhou.myqcloud.com/202409222331310.png)

- 找到最新的发布版本，并下载适用于 Windows 的 ZIP 文件（例如 colmap-3.10-windows.zip）。
**安装 COLMAP**
- 下载 ZIP 文件后，解压到你选择的目录。
  ![image.png](https://pic-1255826935.cos.ap-guangzhou.myqcloud.com/202409222331341.png)

- 进入解压后的目录，找到 COLMAP.bat 文件。
  ![image.png](https://pic-1255826935.cos.ap-guangzhou.myqcloud.com/202409222332936.png)

**运行 COLMAP GUI**
- 双击 COLMAP.bat 文件启动 COLMAP GUI。
  ![image.png](https://pic-1255826935.cos.ap-guangzhou.myqcloud.com/202409222332400.png)

**创建 COLMAP 项目**
- 在 COLMAP GUI 中，创建一个新的项目并导入提取的帧。
- File > New project
- Database :
- Images :
  **特征提取
- 在 COLMAP GUI 中，选择 Processing>Feature Extraction
  ![image.png](https://pic-1255826935.cos.ap-guangzhou.myqcloud.com/202409222343377.png)
- 设置以下参数：
  ![image.png](https://pic-1255826935.cos.ap-guangzhou.myqcloud.com/202409222343954.png)
  ![image.png](https://pic-1255826935.cos.ap-guangzhou.myqcloud.com/202409222347201.png)

- 参数说明
```
## Camera model
选择相机模型。常见的相机模型包括 SIMPLE_RADIAL、PINHOLE 等。你可以根据相机的实际情况选择合适的模型。

## Parameters
Shared for all images：对所有图像使用相同的相机参数。
Shared per sub-folder：对每个子文件夹使用相同的相机参数。
Parameters from EXIF：从图像的 EXIF 数据中提取相机参数。
Custom parameters：手动输入相机参数。

## Extract
mask_path：选择包含掩码图像的文件夹（可选）。
camera_mask_path：选择相机掩码文件（可选）。
max_image_size：设置图像的最大尺寸（例如 3200）。
max_num_features：设置每张图像提取的最大特征数（例如 8192）。
first_octave：设置金字塔的第一个八度（例如 -1）。
num_octaves：设置金字塔的八度数（例如 4）。
octave_resolution：设置每个八度的分辨率（例如 3）。
peak_threshold：设置峰值阈值（例如 0.00667）。
edge_threshold：设置边缘阈值（例如 10.00）。

## Import
import_path 是指你要导入的图像文件夹路径。你需要选择包含视频帧的文件夹，以便 COLMAP 可以从这些图像中提取特征。
```

- 配置完成后，点击 Extract 按钮开始特征提取
  ![image.png](https://pic-1255826935.cos.ap-guangzhou.myqcloud.com/202409222351840.png)

**特征匹配
- 在 COLMAP GUI 中，选择 Feature Matching，并设置以下参数：
- Database Path：选择之前创建的数据库文件（如 database.db）。
- 点击 Run 开始特征匹配。
  **稀疏重建
- 在 COLMAP GUI 中，选择 Sparse Reconstruction，并设置以下参数：
- Image Path：选择包含提取帧的目录。
- Database Path：选择之前创建的数据库文件（如 database.db）。
- Output Path：选择一个输出目录（如 sparse）。
- 点击 Run 开始稀疏重建。
  **导出相机姿态
- 在 COLMAP GUI 中，选择 File -> Export -> Export Model as...，选择 TXT 格式，并导出相机姿态和点云数据。


**使用命令行界面**
- 特征提取
```bash
colmap feature_extractor \
    --database_path database.db \
    --image_path path/to/images \
    --ImageReader.camera_model SIMPLE_RADIAL \
    --ImageReader.single_camera 1
```
- 特征匹配
```bash
colmap exhaustive_matcher \
    --database_path database.db
```
- 稀疏重建
```bash
mkdir sparse
colmap mapper \
    --database_path database.db \
    --image_path path/to/images \
    --output_path sparse
```
- 导出相机姿态
```bash
colmap model_converter \
    --input_path sparse/0 \
    --output_path sparse/0 \
    --output_type TXT
```
- 使用 ffmpeg 提取视频帧
```bash
ffmpeg -i input_video.mp4 -vf "fps=1" frames/frame_%04d.png
```