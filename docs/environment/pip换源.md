# pip 换镜像源

## Ubuntu

临时换源
```terminal
pip install -i https://mirrors.ustc.edu.cn/pypi/web/simple package
```

永久换源
```terminal
pip config set global.index-url https://mirrors.ustc.edu.cn/pypi/web/simple
```

## Windows

直接在user目录中创建一个pip目录，如：C:\Users\xx\pip，在pip 目录下新建文件pip.ini，内容如下

```Text
[global]
timeout = 6000
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
trusted-host = pypi.tuna.tsinghua.edu.cn
```