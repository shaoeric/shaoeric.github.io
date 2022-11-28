# Ubuntu python环境安装

## python3.6安装

```terminal
sudo apt install software-properties-common
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt update
sudo apt install python3.6 #版本自己选择
```
或者 直接安装Miniconda3-4.5.4  4.5.4是最后一个默认python36版本

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

## 创建虚拟环境
```
# virtualenv 创建
virtualenv env_name --python=python3.6

# conda离线创建
conda -n env_name python=3.6 --offline  
```

## 虚拟环境打包
```
# 写入txt文件
pip freeze > requirement.txt

# whl离线包缓存
pip download -d save_dir -r requirement.txt

# 在目标机器上离线安装
pip install --no-index --find-links=save_dir -r requirement.txt
```

## 问题
- No module named 'pip._vendor.six'
    ```
    (test_env) (base) amax@amax:~/4T/4T/clothes_detection_2022$ pip install --no-index --find-links=ubuntu_offline_packages/ -r requirements.txt
    Traceback (most recent call last):
    File "/4T/clothes_detection_2022/test_env/bin/pip", line 5, in <module>
        from pip._internal.cli.main import main
    File "/4T/clothes_detection_2022/test_env/lib/python3.6/site-packages/pip/_internal/cli/main.py", line 10, in <module>
        from pip._internal.cli.autocompletion import autocomplete
    File "/4T/clothes_detection_2022/test_env/lib/python3.6/site-packages/pip/_internal/cli/autocompletion.py", line 9, in <module>
        from pip._internal.cli.main_parser import create_main_parser
    File "/4T/clothes_detection_2022/test_env/lib/python3.6/site-packages/pip/_internal/cli/main_parser.py", line 7, in <module>
        from pip._internal.cli import cmdoptions
    File "/4T/clothes_detection_2022/test_env/lib/python3.6/site-packages/pip/_internal/cli/cmdoptions.py", line 24, in <module>
        from pip._internal.exceptions import CommandError
    File "/4T/clothes_detection_2022/test_env/lib/python3.6/site-packages/pip/_internal/exceptions.py", line 10, in <module>
        from pip._vendor.six import iteritems
    ModuleNotFoundError: No module named 'pip._vendor.six'
    ```

    python3.7以上
    curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py  & python get-pip.py --force-reinstall

    python3.6
    curl https://bootstrap.pypa.io/pip/3.6/get-pip.py -o get-pip.py & python get-pip.py --force-reinstall

- AttributeError: install_layout 及 Running setup.py install for future
    ```
    Preparing metadata (setup.py) ... done
    Building wheels for collected packages: future
    Building wheel for future (setup.py) ... error
    ERROR: Command errored out with exit status 1:
    command: /4T/clothes_detection_2022/test_env/bin/python -u -c 'import io, os, sys, setuptools, tokenize; sys.argv[0] = '"'"'/tmp/pip-req-build-vfaznniw/setup.py'"'"'; __file__='"'"'/tmp/pip-req-build-vfaznniw/setup.py'"'"';f = getattr(tokenize, '"'"'open'"'"', open)(__file__) if os.path.exists(__file__) else io.StringIO('"'"'from setuptools import setup; setup()'"'"');code = f.read().replace('"'"'\r\n'"'"', '"'"'\n'"'"');f.close();exec(compile(code, __file__, '"'"'exec'"'"'))' bdist_wheel -d /tmp/pip-wheel-xmqf17m1
        cwd: /tmp/pip-req-build-vfaznniw/
    ...
    installing to build/bdist.linux-x86_64/wheel
    running install
    running install_lib
    Traceback (most recent call last):
        File "<string>", line 1, in <module>
        ...
        File "/usr/local/python36/lib/python3.6/distutils/cmd.py", line 103, in __getattr__
        raise AttributeError(attr)
        AttributeError: install_layout
        ----------------------------------------
        ERROR: Failed building wheel for future
        Running setup.py clean for future
        Failed to build future
        Installing collected packages: future
            Running setup.py install for future ... error
    ```

    pip install --upgrade setuptools pip
    
    把setuptools库和pip库更新