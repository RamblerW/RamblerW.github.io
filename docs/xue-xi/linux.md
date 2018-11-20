# Linux 学习笔记
> CentOS 7

1. 配置阿里yum源
    1. 查看系统版本
    ```
    cat /etc/redhat-release
    ```
    - 下载aliyun yum源repo文件
    ```
    wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
    ```
    - 清除缓存
    ```
    yum clean all
    ```
    - 把yum源缓存到本地，加快软件的搜索好安装速度
    ```
    yum makecache
    ```
    - 列出 yum 安装包
    ```
    yum list
    ```
- navicat ssh 远程连接 mysql
    1. 新建 mysql 连接，在选项卡里点击“SSH”
    - SSH的默认端口是22，这里的用户名和密码应该是在CentOS上拥有FTP权限的用户名和密码
    - 填写“常规”选项卡，主机名/IP地址一定要填写<font color=red>“localhost”或者“127.0.0.1”</font>，用户名和密码是远程MySQL数据库的用户名和密码
- yum 安装 jdk，配置环境变量
    1. 查看系统自带的 jdk 是否已安装
    ```
    yum list installed |grep java
    ```
    - 查看yum库中的Java安装包
    ```
    yum -y list java*
    ```
    - 将java-1.8.0的所有相关Java程序都安装上
    ```
    yum -y install java-1.8.0-openjdk*
    ```
    - 查看 java 版本
    ```
    java -version
    ```
    - 配置环境变量
    ```
    vi /etc/profile
    #
    # 在文件最后加入如下行
    #
    #java
    JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.171-8.b10.el7_5.x86_64
    CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
    PATH=$JAVA_HOME/bin:$PATH:
    export JAVA_HOME
    export CLASSPATH
    export PATH
    #
    # 保存关闭,执行如下命令使设置生效
    #
    source  /etc/profile
    #
    # 使用以下命令,查看变量
    #
    echo $JAVA_HOME
    ```
- 查看 java 进程
```
ps -ef | grep java
```
- 强制杀死进程
```
kill -s 9 进程号
```
- 终端浏览器 w3m
```
yum -y install w3m w3m-img
```
- 上传下载文件
```
yum -y install lrzsz
# 下载
sz filename
# 上传
rz
```
- 配置 python3 环境
    1. yum 安装 python3
    ```
    # 添加epel源
    sudo yum install epel-release
    # 安装 python3
    sudo yum install python34
    ```
    - 安装 pip3
    ```
    yum install python34-setuptools
    easy_install-3.4 pip
    ```
    