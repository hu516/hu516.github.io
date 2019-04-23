1. 在桌面空白处点击右键菜单"打开终端" ；
2. 输入命令`sudo passwd root`，按照提示为root用户设置密码；
3. 输入命令`su`，输入root用户密码 ；
4. 输入命令`sudo apt -y install openssh-server`， 等待完成openssh-server安装；
5. 安装完毕，运行命令`vi /etc/ssh/sshd_config`；
6. 在行"#PermitRootLogin prohibit-password"后， 添加行 "PermitRootLogin yes"，并保存；
7. 输入命令`sudo service sshd start`启动服务;
8. 输入命令`sudo service sshd status`查看服务运行状态，"active(running)"说明服务正常。
