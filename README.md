# 目标检测项目

## 如何进行目标检测

### 1. 环境准备
在开始之前，请确保您的环境中已安装必要的依赖项。可以通过运行以下命令来安装所需的软件包：
```bash
pip install -r requirements.txt
```

### 2. 数据准备
请将您的数据整理为标准格式，并置于该文件夹上层目录中的`datasets`文件夹（需要新建）下，然后撰写数据集yaml配置文件并将其放置于`data`目录下。

```angular2html
# my_custom_dataset.yaml
path: ../datasets/my_custom_dataset  # dataset root dir
train: images/train  # train images (relative to 'path')
val: images/val  # val images (relative to 'path')
#test: images/test  # test images (relative to 'path')

names:
  0: Not Weighed
  1: Weighed

# Download script/URL (optional)
# 如果你需要自动下载脚本或URL，可以在这里添加。对于本地数据集，这个字段通常是不需要的。
# download: [your_download_link_or_script]
```

### 3. 模型训练
您可以使用`train.py`脚本来训练您的目标检测模型。以下是基本的训练命令示例：
```bash
python train.py --data your_dataset.yaml --cfg yolov5s.yaml --weights yolov5s.pt
```
- `--data`: 指定数据集配置文件的路径。
- `--cfg`: 模型配置文件的路径。
- `--weights`: 预训练权重的路径，可用于迁移学习。

### 4. 模型评估
训练完成后，可以使用`val.py`脚本来验证模型性能：
```bash
python val.py --weights runs/train/exp/weights/best.pt --data your_dataset.yaml
```

### 5. 目标检测演示
对于已经训练好的模型，您可以使用`detect.py`脚本来执行目标检测任务：
```bash
python detect.py --source 0  # 使用摄像头
# 或者
python detect.py --source path/to/image.jpg  # 使用图片文件
```

### 6. 导出模型
如果需要将模型导出以供其他平台使用，可以利用`export.py`脚本完成这一操作：
```bash
python export.py --weights best.pt --include torchscript onnx
```
