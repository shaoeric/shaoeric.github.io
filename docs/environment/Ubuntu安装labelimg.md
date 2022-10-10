# Ubuntu安装labelimg

- github仓库克隆到本地
```shell
git clone https://github.com/Ruolingdeng/labelImg.git
```

- 进入到labelimg文件夹
```shell
cd labelimg-master/
```

- 安装pyqt依赖包
```shell
sudo apt-get install pyqt5-dev-tools
```

- 在labelimg-master目录下，安装requirements依赖包
```shell
pip instsall -r requirements/requirements-linux-python3.txt
```

- 在label-master目录下进行编译
```shell
make qt5py3
```

- 运行测试
```shell
python labelImg.py
```