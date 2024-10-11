---
layout:       post
title:        "pip install mysqlclient安装mysqlclient的时候报错"
author:       "Seanqian"
header-style: text
catalog:      true
tags:
    - pip 
    - pip install
    - mysqlclient
    - pip install mysqlclient报错

---

##### 现象1
在安装mysqlclient的时候报错，报错信息如下：
```
ERROR: Could not find a version that satisfies the requirement mysqlclient (from versions: none)
ERROR: No matching distribution found for mysqlclient
```

##### 解决方法
1. 下载mysqlclient的源码包，下载地址为：https://github.com/PyMySQL/mysqlclient-python/releases
2. 解压下载的源码包，进入解压后的目录
3. 执行以下命令：
```
python setup.py install
```
4. 安装完成后，再次执行pip install mysqlclient，应该就不会报错了。


##### 如果刚才没什么用

如果报错信息是这样的：
```
note: This error originates from a subprocess, and is likely not a problem with pip.
error: subprocess-exited-with-error

    × Getting requirements to build wheel did not run successfully.
    │ exit code: 1
    ╰─> See above for output.

note: This error originates from a subprocess, and is likely not a problem with pip.
```
    
    
为了解决安装mysqlclient库的依赖库,要根据操作系统来安装:

##### ubuntu安装mysqlclient环境

    sudo apt-get install python3-dev default-libmysqlclient-dev build-essential pkg-config

-  安装好环境再pip install mysqlclient即可

##### centos安装mysqlclient环境
    mysqlclient安装失败要先安装mysql-devel

    yum install mysql-devel  python3-devel  gcc

##### 树莓派安装mysqlclient环境
    在raspi4b上面如果需要安装mysqlclient的包

    必须在之前安装下面的包

    sudo apt-get install default-lib mysqlclient-dev  

    apt-get install build-essential

##### mac安装mysqlclient环境
    用brew install mysql-client，然后brew info mysql-client，有提示

    根据提示将如下示例运行：

    export PKG_CONFIG_PATH="/usr/local/opt/mysql-client/lib/pkgconfig”

    m3芯片的mac有时安装好了pkg-config提示还是找不到，就需要再运行一下下面的命令：

    export PKG_CONFIG_PATH=$(find /opt/homebrew/Cellar -name 'pkgconfig' -type d | grep lib/pkgconfig | tr '\n' ':' | sed s/.$//)


- 总之先安装各个不同操作系统的依赖就好