
Install pip3 for Python3.X(With Python2.7)
================

###### `how to install pip3 for python3.x`
  
  ```
  重要的事情说三遍：
  如果你不知道你在做什么，千万不要动系统自带的Python2.7，也不要修改命令行默认的Python命令版本！
  如果你不知道你在做什么，千万不要动系统自带的Python2.7，也不要修改命令行默认的Python命令版本！
  如果你不知道你在做什么，千万不要动系统自带的Python2.7，也不要修改命令行默认的Python命令版本！
  ```

  在Kali Linux上：`Kali上同时自带Python2.7和Python3.6`。</br>
  在默认命令行状态下，python执行的是2.7版本，然而一些新的第三方库有时需要使用Python3.X的版本；
  这就出现了一定的问题：比如我要使用beautifulsoup，发现Pycharm(Python3.6)下执行：
  ```Python
  from bs4 import BeautifulSoup
  ```
  会报错，提示无法找到BeautifulSoup。但是在命令行下，执行：
  ```
  python from bs4 import BeautifulSoup
  ```
  是没有问题的。那么原因出现在什么地方呢？</br>
  原因在于：`BeautifulSoup安装在Python2.7版本下，而Python3.X下则没有`，</br>
  那么是否直接执行以下命令就行了呢？
  ```
  pip3 install BeautifulSoup4
  ```
  很遗憾...没有pip3命令...那么安装pip3？很遗憾...找不到setuptools....GG!</br>
  针对这个问题，我也在网上搜了一些结果，可是大部分结果要不环境不一样...要不执行完没有效果...</br>
  经整理，以下解决办法经过测试有效！
  ```
  Linux版本：Kali 2.0
  Python版本：Python3.6（并存Python2.7）
  ```

------------------------------------

# 一、Pre:Install python3 （for !Kali）
  
  --> 下载Python3.X
  ```
  # wget https://www.python.org/ftp/python/3.6.1/Python-3.6.1.tar.xz
  ```
  
  --> 安装依赖
  ```
  # yum -y install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel
  ```
  
  --> 解压
  ```
  # tar -zxvf Python-3.6.1.tar.xz
  ```
  
  --> 预建立文件夹（安装位置随意，我一般安装在opt下）
  ```
  # mkdir -p /opt/python3
  ```
  
  --> 进入解压目录，安装
  编译
  ```
  # cd /root/Python-3.6.1
  # ./configure --prefix=/opt/python3
  ```
  Make & Make Install
  ```
  # make && make install
  ```

  --> 建立软链
  ```
  # ln -s /opt/python3/bin/python3 /usr/bin/python3
  ```

  --> 加入PATH（可选）
  修改
  ```
  # vim ~/.bash_profile
  # .bash_profile
  # Get the aliases and functions
  if [ -f ~/.bashrc ]; then
  . ~/.bashrc
  fi
  # User specific environment and startup programs
  PATH=$PATH:$HOME/bin:/usr/local/python3/bin
  export PATH
  ```
  生效
  ```
  # source ~/.bash_profile
  ```
  
  --> 验证
  ```
  # python3 -V
  ```
  
  

## 4.编译安装

！！！！注意 注意 ⚠️  在编译之前需要安装一些必须的依赖，否则当报错的时候还得重新编译 －－－（我就是吃了这个亏，千万要注意奥。。。）

安装必要依赖（至少需要如下两个，我个人就遇到如下两个）



好了现在可以安心的编译咯：

cd Python-3.5.2
./configure --prefix=/opt/Python     #安装目录可以自己定义无所谓。
make
make install

编译完成后会在如 /opt/下生成Python的文件夹 ，没错这就是编译完成的python  －－为了方便之行小伙伴们可以自己定义一个软连接如下：

# ln -s /opt/Python/bin/python3 /usr/bin/python3

这样就可以直接食用python3了如下：

　　　　　　　　　　

好到目前为止，我们在linux下安装python3的任务已经完成，下面进入关键的地方，给python3安装pip3

二.install pip for python3.x

其实这也不难。。下载量个包，执行两个命令搞定。

1.首先安装setuptools

　　小伙伴们可以通过官方模块库来下载：https://pypi.python.org/pypi

　　这里我就直接用wget到服务器上下载了版本为19.6（小伙伴们可以尝试新的版本奥。。）
复制代码

wget --no-check-certificate  https://pypi.python.org/packages/source/s/setuptools/setuptools-19.6.tar.gz#md5=c607dd118eae682c44ed146367a17e26

tar -zxvf setuptools-19.6.tar.gz

cd setuptools-19.6.tar.gz

python3 setup.py build

python3 setup.py install

复制代码

2.然后直接安装pip就搞定了。。

　　同样先下载然后在执行命令搞定！！
复制代码

wget --no-check-certificate  https://pypi.python.org/packages/source/p/pip/pip-8.0.2.tar.gz#md5=3a73c4188f8dbad6a1e6f6d44d117eeb

tar -zxvf pip-8.0.2.tar.gz

cd pip-8.0.2

python3 setup.py build

python3 setup.py install

复制代码

安装完成之后我们再来看下python的bin目录下都有什么东西吧

哈哈。。通过以上我们已经给python3安装好了 pip3了。。。（小伙伴们也可以做个软连接，来方便实用奥。。）

 
三。来做个测试吧

1.首先我们进入pytho3
复制代码

[root@centos3 bin]# python3
Python 3.5.2 (default, Jul 27 2016, 03:36:56) 
[GCC 4.4.7 20120313 (Red Hat 4.4.7-4)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import pymysql
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ImportError: No module named 'pymysql'   ##没有此模块奥
>>> 

复制代码

好 ，我们用新安装的pip3来装下试试：
复制代码

[root@centos3 bin]# /opt/Python/bin/pip3 install pymysql
Collecting pymysql
  Downloading PyMySQL-0.7.5-py2.py3-none-any.whl (77kB)
    100% |████████████████████████████████| 81kB 3.2kB/s 
Installing collected packages: pymysql
Successfully installed pymysql-0.7.5

######安装完成

复制代码

安装完成了，看来pip3本身没有问题，我们测试下是否真正的给python3装上了这个模块吧（有可能装到了python2上了呢 ……-_-#）
复制代码

[root@centos3 bin]# python3
Python 3.5.2 (default, Jul 27 2016, 03:36:56) 
[GCC 4.4.7 20120313 (Red Hat 4.4.7-4)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import pymysql
>>> 

复制代码

哈哈哈 ok了。。 结束！！

 
