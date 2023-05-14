# 手动安装和部署发开环境
进入华为昇腾社区 https://www.hiascend.com/

进入root
下载环境包
200dk制卡用的操作系统 http://old-releases.ubuntu.com/releases/18.04.4/?_ga=2.44113060.1243545826.1617173008-2055924693.1608557140 
buntu-18.04-server-arm64.iso	2018-04-26 18:32 	670M

下载200dk的驱动（CANN 6.0.0.alpha001）
https://www.hiascend.com/zh/hardware/firmware-drivers/community?product=5&model=6&cann=6.0.0.alpha001&driver=1.0.13.alpha

200dk推理包
https://www.hiascend.com/software/cann/community-history
Ascend-cann-nnrt_6.0.0.alpha001_linux-aarch64.run
Ascend-cann-toolkit_6.0.0.alpha001_linux-aarch64.run

开发环境包（x86）
Ascend-cann-toolkit_6.0.0.alpha001_linux-x86_64.run

环境部署
制卡操作
https://www.hiascend.com/document/detail/zh/Atlas200DKDeveloperKit/1013/environment/atlased_04_0010.html
选择环境部署-制作SD卡-读卡器场景-操作步骤5
wget https://gitee.com/ascend/tools/raw/master/makesd/generic_script/make_sd_card.py
wget https://gitee.com/ascend/tools/raw/master/makesd/generic_script/make_ubuntu_sd.sh

连接操作（连接Altas 200 DK开发板与Ubuntu服务器）
https://gitee.com/ascend/tools/blob/master/configure_usb_ethernet/for_20.1/configure_usb_ethernet.sh
右上角原始数据save link as

python3.7.5源码包
wget https://www.python.org/ftp/python/3.7.5/Python-3.7.5.tgz

将以上一共9个依赖包放置在一个目录下

制卡步骤
https://www.hiascend.com/document/detail/zh/Atlas200DKDeveloperKit/1013/environment/atlased_04_0010.html
执行如下命令安装相关python依赖：
apt install python3-pip
pip3 install pyyaml
apt-get install qemu-user-static binfmt-support python3-yaml squashfs-tools gcc-aarch64-linux-gnu g++-aarch64-linux-gnu

将SD卡插入至ubuntu
查看SD卡被挂载到ubuntu哪个路径下，复制一下
fdisk -l
在所有依赖包的
python3 make_sd_card.py local /dev/sdb 后面是SD卡的挂载路径
需要等待漫长的时间直至出现 Make SD Card successfully！

拔出读卡器，拔出SD Card插入到200dk，接上电源，等待数分钟直至开发板上的四个指示灯全亮起

安装开发环境
sudo apt-get install -y gcc g++ make cmake zlib1g zlib1g-dev libbz2-dev libsqlite3-dev libssl-dev libxslt1-dev libffi-dev unzip pciutils net-tools libncursesw5-dev 

编译安装python3.7.5
exit到普通用户下
tar zxvf Python-3.7.5.tgz
cd Python-3.7.5
配置
./configure --prefix=/usr/local/python3.7.5 --enable-loadable-sqlite-extensions --enable-shared

编译
make -j8

安装
sudo make install

sudo ln -s /usr/local/python3.7.5/bin/python3 /usr/local/python3.7.5/bin/python3.7.5
sudo ln -s /usr/local/python3.7.5/bin/pip3 /usr/local/python3.7.5/bin/pip3.7.5

设置python3.7.5环境变量
vim ~/.bashrc

#用于设置python3.7.5库文件路径
export LD_LIBRARY_PATH=/usr/local/python3.7.5/lib:$LD_LIBRARY_PATH
#如果用户环境存在多个python3版本，则指定使用python3.7.5版本
export PATH=/usr/local/python3.7.5/bin:$PATH

source ~/.bashrc

安装python3相关依赖
pip3.7.5 install attrs psutil decorator numpy protobuf==3.11.3 scipy sympy cffi --user

安装开发环境包
chmod +x *.run
./Ascend-cann-toolkit_6.0.0.alpha001_linux-x86_64.run --install

复制 'lease make sure that:' 之后的内容保存到一个文件里面
vim env.txt

./Ascend-cann-toolkit_6.0.0.alpha001_linux-aarch64.run --install

至此开发环境基本安装完成



