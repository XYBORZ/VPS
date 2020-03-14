修改了逗比一键ssr脚本的默认参数，方便搭建免流服务器。（一路回车到底，顺畅无比。）

一、设置root密码
打开ssh连接vps
切换到root账号   sudo -i
设置root密码   passwd
然后会要求输入新密码，然后再重复一次密码，输入密码的时候不会显示出来，所以直接输入密码，然后回车，再然后重复输入密码回车。

二、开启SSH权限
方法一
修改SSH配置文件
vi /etc/ssh/sshd_config
然后再输”i”进入编辑模式
找到以下内容并修改
PermitRootLogin yes           //默认为no，需要开启root用户访问改为yes
PasswordAuthentication yes    //默认为no，改为yes开启密码登陆
修改完成后，再下按 esc 键，然后再输入
:wq
重启SSH服务
service sshd restart
方法二
CentOS和Debian通用，输入以下两条命令
sed -i 's/PermitRootLogin no/PermitRootLogin yes/g' /etc/ssh/sshd_config
sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
Ubuntu系统，输入以下两条命令
sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/g' /etc/ssh/sshd_config
sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
重启服务器
reboot
推荐方法二。

wget -N --no-check-certificate https://raw.githubusercontent.com/XYBORZ/VPS/master/ssr.sh && chmod +x ssr.sh && bash ssr.sh
