# my_mmrotate
修改了一些模型配置，自定义一些可插入组件，运行最新的一些模型
```
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple torch==1.13.1+cu116 torchvision==0.14.1+cu116 torchaudio==0.13.1 --extra-index-url https://download.pytorch.org/whl/cu116
```
torch最好用1.13不然会有问题。

```
pip install openmim
mim install mmengine
mim install "mmcv==2.0.0rc4"

mim install "mmcls==1.0.0rc6"
mim install "mmdet>=3.0.0rc2"
```

进入mmrotate文件夹
```
pip install -r requirements.txt　　　　　　　　
pip install -v -e .
pip install -U Pillow
```

enn依赖有可能在服务器上git不下来，用不上就可以不装