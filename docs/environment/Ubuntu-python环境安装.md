# Ubuntu python环境安装

## python3.6安装

```terminal
sudo apt install software-properties-common
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt update
sudo apt install python3.6 #版本自己选择
```

## 安装python3.6对应的pip
```terminal
curl https://bootstrap.pypa.io/pip/3.6/get-pip.py -o "get-pip.py"
python3.6 get-pip.py
```

## 添加环境变量
```terminal
sudo gedit ~/.bashrc
export PATH=/usr/local/python36/bin:$PATH
source ~/.bashrc
```

或建立软链接
```
sudo ln -s -f /usr/local/python36/bin/python3.6 /usr/bin/python3
sudo ln -s -f /usr/local/python36/bin/pip3.6 /usr/bin/pip3
sudo ln -s -f /usr/local/python36/bin/python3.6 /usr/bin/python
sudo ln -s -f /usr/local/python36/bin/pip3.6 /usr/bin/pip
```

## 虚拟环境
```
sudo apt install python3-virtualenv
sudo apt install python3.6-distutils
```