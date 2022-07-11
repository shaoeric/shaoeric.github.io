# ubuntu挂载硬盘

- 查看硬盘情况
```terminal
df -h
```

    ```Text
    文件系统        容量  已用  可用 已用% 挂载点
    udev             16G     0   16G    0% /dev
    ---
    /dev/sdb2       3.2T  ---
    ```
sdb2是我们要挂载的硬盘，我们期望它被挂载到`/4T`目录上

- 创建挂载位置
```terminal
mkdir /4T
# 修改权限
sudo chmod -R 777 /4T
```

- 获取挂载分区的UUID和分区类型
```terminal
sudo blkid
```

    ```Text
/dev/sdb2: UUID="361xxxxxx" TYPE="ext4" PARTUUID="8e87xxxxxx"
    ```

- 挂载硬盘
```terminal
sudo mount -t ext4 /dev/sdb2
```

- 自动挂载
    ```terminal
sudo gedit /etc/fstab

    # 添加一行
UUID=361xxxxxx /4T ext4 defaults 0 2
    ```

- 全部挂载
```terminal
sudo mount -a
```