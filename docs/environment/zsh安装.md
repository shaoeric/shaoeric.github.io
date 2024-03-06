# ZSH安装

## zsh

[zsh仓库](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH)

```shell
# ubuntu
apt install zsh

# centos
yum -y install zsh
```

查看zsh
```
$ which zsh      
/usr/bin/zsh
```

## 安装oh my zsh
```shell
# 参考https://github.com/ohmyzsh/ohmyzsh#basic-installation
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

- 配置主题

参考[链接](https://github.com/ohmyzsh/ohmyzsh#selecting-a-theme)

```shell
vim ~/.zshrc
# 修改 ZSH_THEME="ys"
```

- 配置Plugins

安装自动补全插件

```shell
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

安装语法高亮
```shell
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

配置
```shell
vim ~/.zshrc
# 修改plugins=(git zsh-autosuggestions zsh-syntax-highlighting)
```

开启zsh
```shell
cd .oh-my-zsh/ && chmod 744 oh-my-zsh.sh
zsh
```