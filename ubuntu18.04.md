# Ubuntu 18.04 

安装ubuntu18.04 https://blog.csdn.net/weixin_43233550/article/details/115417176

可能存在的安装报错 https://blog.csdn.net/lezeqe/article/details/83447690

安装vmware-tools https://blog.csdn.net/thy0000/article/details/122638884

更改root密码 sudo passwd root

更换源（如果身处中国） http://www.cnblogs.com/fanbi/p/10423080.html bionic意思是ubuntu18
su root 进入root模式
cd /etc/apt 进入该改路径下 ls查看当前目录下的文件
cp sources.list sources.list.bak 复制一下，备个份
清空sources.list >sources.list
vi sources.list 修改内容
输入 i 粘贴内容 esc :wq
apt-get update 更新下载软件的索引

安装vim apt-get install vim 
输入vim验证是否安装完成 :q退出

