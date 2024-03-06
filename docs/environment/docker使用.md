# docker使用

## 安装nvidia-docker
```shell
curl https://get.docker.com | sh && sudo systemctl --now enable docker
distribution=$(. /etc/os-release;echo $ID$VERSION_ID) && curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg && curl -s -L https://nvidia.github.io/libnvidia-container/experimental/$distribution/libnvidia-container.list | sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
sudo apt-get update
sudo apt-get install -y nvidia-docker2
sudo systemctl restart docker
sudo docker run --rm --gpus all nvidia/cuda:11.0.3-base-ubuntu20.04 nvidia-smi
```

## 使用

- 将宿主机的12334端口映射到容器的5678端口。
```shell
nvidia-docker run -it -p 1234:5678 nvidia/cuda:11.0.3-base-ubuntu20.04
```

- 打包构建

```Dockerfile
FROM nvidia/cuda:11.0.3-base-ubuntu20.04 # 拉取镜像
RUN mkdir -p /home/
COPY Miniconda3-py37_4.10.3-Linux-x86_64.sh /home 
COPY requirement.txt /home/
RUN cd /home && bash Miniconda3-py37_4.10.3-Linux-x86_64.sh -b -p /miniconda3 && rm Miniconda3-py37_4.10.3-Linux-x86_64.sh
ENV PATH=/miniconda3/bin:$PATH

RUN /miniconda3/bin/pip install -r /home/requirement.txt -i https://pypi.tuna.tsinghua.edu.cn/simple/ && rm /home/requirement.txt
WORKDIR /home
```

- 执行

```shell
sudo docker build -t docker_name . # 打包镜像
sudo nvidia-docker run -p 1234:5678 -it docker_name /bin/bash # 启动并进入容器
sudo docker exec -it container_id /bin/bash  # 进入容器

sudo docker stop container_id # 停止容器
sudo docker start container_id # 启动容器
```

## 在docker file中安装oh my zsh

```Dockerfile
RUN yum update -y
RUN yum -y install zsh
RUN yum install tmux -y
RUN echo "Y" | sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
RUN chsh -s /bin/zsh
RUN sed -i 's/ZSH_THEME=.*/ZSH_THEME="ys"/' ~/.zshrc
RUN sed -i 's/plugins=.*/plugins=(git zsh-autosuggestions zsh-syntax-highlighting z colored-man-pages tmux)/' ~/.zshrc
RUN git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
RUN git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
RUN cat $HOME/.bashrc >> $HOME/.zshrc
```
然后在.zshrc中删除和bash相关的命令