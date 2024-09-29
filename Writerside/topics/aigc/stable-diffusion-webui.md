## 仓库地址
 - [stable-diffusion-webui](https://github.com/AUTOMATIC1111/stable-diffusion-webui)
## 使用 docker 运行
```bash
docker run --detach \
--name sd-webui \
--gpus all \
--restart always \
--publish 8080:8080 \
--volume $HOME/.sd-webui/models:/app/stable-diffusion-webui/models \
--volume $HOME/.sd-webui/extensions:/app/stable-diffusion-webui/extensions \
--volume $HOME/.sd-webui/outputs:/app/stable-diffusion-webui/outputs \
--volume $HOME/.sd-webui/localizations:/app/stable-diffusion-webui/localizations \
universonic/stable-diffusion-webui
```
```powershell
docker run --detach `
--name sd-webui `
--gpus all `
--restart always `
--publish 8080:8080 `
--volume $HOME/.sd-webui/models:/app/stable-diffusion-webui/models `
--volume $HOME/.sd-webui/extensions:/app/stable-diffusion-webui/extensions `
--volume $HOME/.sd-webui/outputs:/app/stable-diffusion-webui/outputs `
--volume $HOME/.sd-webui/localizations:/app/stable-diffusion-webui/localizations `
universonic/stable-diffusion-webui
```

## 中文语言包设置
- https://github.com/dtlnor/stable-diffusion-webui-localization-zh_CN
- 将文件下载后放到 stable-diffusion-webui/localizations/zh_CN.json 里面
- 打开页面 > Settings > User Interface >Localization > 选择 zh_CN > Apply Settings > Reload UI

## 安装插件方法
- 进入 stable-diffusion-webui/extensions 目录
- git clone 插件地址
- 重启 UI

## 中文提示词翻译插件
- https://github.com/studyzy/sd-prompt-translator

## 正向提示词参考
```
stunning environment / 令人惊讶的环境 / 让AI根据其他关键字做出充满创造力的风景
aerial view / 空中鸟瞰 / 鸟瞰远景镜头
landscape / 风景画 / 通常是山野风情画背景
aerial photography / 鸟瞰绘图 / 类似aerial view
massive scale / 宏伟构图 / 建筑物的密度与高度有可能被夸大
street level view / 街头景色 / 从路面上平视的街景
lush vegetation / 植物茂盛 / 植物茂盛的景色
idyllic / 瑞士乡间 / 理想退休人士居住的天堂般宁静乡间
overhead shot / 正上方鸟瞰 / 正上方或斜上方视角
Matte painting / 接景 / 将数种风景地貌拼接在一起
blurry background / 模糊背景 / 将背景模糊创造聚焦效果
```
## 细节描写
```bash
wallpaper / 壁纸
poster / 挂报
sharp focus / 鋭焦
hyperrealism / 超写实主义
insanely detailed / 密密麻麻的细节
lush detail / LUSH化妆品美颜
filigree / 植物纹精工金饰
intricate / 丝线精工金饰
crystalline / 水晶首饰
perfectionism / 完美主义
max detail / 最大化细节
spirals / 漩涡纹
tendrils / 植物首饰
ornate / 复杂装饰纹
angelic / 天使般
decorations / 盛装
embellishments / 礼服镶嵌碎花
hard edge / 棱角分明
breathtaking / 令人屏息
embroidery / 刺綉
tiara / 王冠
```

## 负面提示词参考
```bash
easy negative,worst quality,low quality,normal quality,lowers,monochrome,grayscales,skin spots,acnes,skin blemishes,age spot,6 more fingers on one hand,deformity,bad legs,error legs,bad feet,malformed limbs,extra limbs,ugly,poorly drawn hands,poorly drawn feet.poorly drawn face,text,mutilated,extra fingers,mutated hands,mutation,bad anatomy,cloned face,disfigured,fused fingers
```

```bash
easy negative / 简单负面
worst quality / 最差品质
low quality / 低品质
normal quality / 正常品质
lowers / 降低
monochrome / 单色
grayscales / 灰阶
skin spots / 皮肤斑点
acnes / 脓疮，痘疤
skin blemishes / 皮肤瑕疵
age spot / 老人斑
6 more fingers on one hand / 多手指
deformity / 畸形
bad legs / 畸形腿
error legs / 错腿
bad feet / 脚型不正
malformed limbs / 畸形四肢
extra limbs / 多余肢体
ugly / 丑
poorly drawn hands / 差劲画技的手
poorly drawn feet / 差劲画技的足
poorly drawn face / 差劲画技的脸
text / 文字
mutilated / 伤口
extra fingers / 多余手指
mutated hands / 突变手掌
mutation / 突变
bad anatomy / 差劲生理结构
cloned face / 重复面孔
disfigured / 变形
fused fingers / 手指融合
```