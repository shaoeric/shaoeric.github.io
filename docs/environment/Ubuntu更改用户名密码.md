# Ubuntu更改用户名密码

- 重启Ubuntu系统，长按Shift进入grub菜单
- 选择`Ubuntu高级选项`
- 选择`recovery mode`,按`e`键进入编辑界面
- 找到`recovery nomodeset`并将其删掉，在该行的最后输入`quiet splash rw init=/bin/bash`
- 按下`F10`进行启动
- 在黑板框的命令行中输入`passwd`+`登录的用户名`，表示修改该用户名的密码
- 按提示连续输入2次密码，按`enter`确认修改密码