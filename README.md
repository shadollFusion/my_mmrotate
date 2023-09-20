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

在autodl服务器上跑DOTA，先在auto-tmp中创建DOTA文件夹
```
# train dataset
unzip -d ~/autodl-tmp/DOTA/train/ ~/autodl-pub/DOTA/train/images/part1.zip
unzip -d ~/autodl-tmp/DOTA/train/ ~/autodl-pub/DOTA/train/images/part2.zip
unzip -d ~/autodl-tmp/DOTA/train/ ~/autodl-pub/DOTA/train/images/part3.zip
unzip -d ~/autodl-tmp/DOTA/train/labelTxt1_0 ~/autodl-pub/DOTA/train/labelTxt-v1.0/labelTxt.zip

# val dataset
unzip -d ~/autodl-tmp/DOTA/val/ ~/autodl-pub/DOTA/val/images/part1.zip
unzip -d ~/autodl-tmp/DOTA/val/labelTxt1_0 ~/autodl-pub/DOTA/val/labelTxt-v1.0/labelTxt.zip

# test dataset
unzip -d ~/autodl-tmp/DOTA/test/ ~/autodl-pub/DOTA/test/images/DOTA_test_part1.zip
unzip -d ~/autodl-tmp/DOTA/test/ ~/autodl-pub/DOTA/test/images/DOTA_test_part2.zip
cp ~/autodl-pub/DOTA/test/images/DOTA_test_test_info.json ~/autodl-tmp/DOTA/test/
```
将mmrotate内置的切图工具放入数据盘方便操作
```
cp -r ~/mmrotate/tools/data ~/autodl-tmp/
```
切割图片
```
# 切train单尺度
python ./autodl-tmp/data/dota/split/img_split.py --base-json \
   ./autodl-tmp/data/dota/split/split_configs/ss_train.json
# 切验证集合
python data/dota/split/img_split.py --base-json \
  data/dota/split/split_configs/ss_val.json
# 切test单尺度
python ./autodl-tmp/data/dota/split/img_split.py --base-json \
  ./autodl-tmp/data/dota/split/split_configs/ss_test.json

# 切train多尺度
python data/dota/split/img_split.py --base-json \
  data/dota/split/split_configs/ms_train.json
# 切test用ms多尺度
python data/dota/split/img_split.py --base-json \
  data/dota/split/split_configs/ms_test.json
```

测复杂度
```
python tools/analysis_tools/get_flops.py configs/s2anet/s2anet-le135_r50_fpn_1x_dota.py --shape 1024 1024
```