
Install pip3 for Python3.X(With Python2.7)
================

###### how to install pip3 for python3.x
  
  ```
  重要的事情说三遍：
  如果你不知道你在做什么，千万不要动系统自带的Python2.7，也不要修改命令行默认的Python命令版本！
  如果你不知道你在做什么，千万不要动系统自带的Python2.7，也不要修改命令行默认的Python命令版本！
  如果你不知道你在做什么，千万不要动系统自带的Python2.7，也不要修改命令行默认的Python命令版本！
  ```

-----------------------------------------------------------------------------------------

  在Kali Linux上：`Kali上同时自带Python2.7和Python3.6`。</br>
  在默认命令行状态下，python执行的是2.7版本，然而一些新的第三方库有时需要使用Python3.X的版本；</br>
  这就出现了一定的问题：比如我要使用beautifulsoup，发现Pycharm(Python3.6)下执行：</br>
  ```Python
  from bs4 import BeautifulSoup
  ```
  会报错，提示无法找到BeautifulSoup。但是在命令行下，执行：</br>
  ```
  python from bs4 import BeautifulSoup
  ```
  是没有问题的。那么原因出现在什么地方呢？</br>
  原因在于：`BeautifulSoup安装在Python2.7版本下，而Python3.X下则没有`</br>
  那么是否直接执行以下命令就行了呢？</br>
  ```
  pip3 install BeautifulSoup4
  ```
  很遗憾...没有pip3命令...那么安装pip3？很遗憾...找不到setuptools....GG!</br>
  针对这个问题，我也在网上搜了一些结果，可是大部分结果要不环境不一样...要不执行完没有效果...</br>
  经整理，以下解决办法经过测试有效！</br>
  ```
  Linux版本：Kali 2.0
  Python版本：Python3.6（并存Python2.7）
  ```
------------------------------------

# 一、Pre: Install python3 （for !Kali）
  
  --> 下载Python3.X
  ```
  # wget https://www.python.org/ftp/python/3.6.1/Python-3.6.3.tar.xz
  ```
  
  
  --> 安装依赖
  ```
  # yum -y install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel
  ```
  
  
  --> 解压
  ```
  # tar -zxvf Python-3.6.3.tar.xz
  ```
  
  
  --> 预建立文件夹（安装位置随意，我一般安装在opt下）
  ```
  # mkdir -p /opt/python3
  ```
  
  
  --> 进入解压目录，安装</br>
  
  编译
  ```
  # cd /root/Python-3.6.3
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


  --> 加入PATH（可选）</br>
  
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
  
# 二、Pre: Install setuptools

  --> 下载setuptools 36.6.0（Up to NOW）
  ```
  wget --no-check-certificate  https://pypi.python.org/packages/45/29/8814bf414e7cd1031e1a3c8a4169218376e284ea2553cc0822a6ea1c2d78/setuptools-36.6.0.zip#md5=74663b15117d9a2cc5295d76011e6fd1
  ```
  
  --> 安装
  ```
  # unzip setuptools-36.6.0.zip

  # cd setuptools-36.6.0

  # python3 setup.py build

  # python3 setup.py install
  ```

# 三、Install pip3

  --> 下载pip-9.0.1（Up to NOW）
  ```
  wget --no-check-certificate  https://pypi.python.org/packages/11/b6/abcb525026a4be042b486df43905d6893fb04f05aac21c32c638e939e447/pip-9.0.1.tar.gz#md5=35f01da33009719497f01a4ba69d63c9
  ```
  
  --> 安装
  ```
  tar -zxvf pip-9.0.1.tar.gz

  cd pip-9.0.1

  python3 setup.py build

  python3 setup.py install
  ```

  --> 建立软链
  ```
  # ln -s /opt/python3/bin/pip3 /usr/bin/pip3
  ```
  
  --> 验证
  ```
  # pip3 -V
  ```

# 四、Verification

  --> 模块验证
  ```
  # python3
  >>> from bs4 import BeautifulSoup
  ```

  --> 命令安装验证
  ```
  # pip3 install pymysql
  ```



FINISH！
===============================================
 
