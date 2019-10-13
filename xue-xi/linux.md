> CentOS 7

- 常用命令

    - 查看端口占用：`netstat -tunlp|grep 端口号`

- 配置阿里yum源

    - 查看系统版本：`cat /etc/redhat-release`

    - 下载aliyun yum源repo文件：`wget -O /etc/yum.repos.d/CentOS-Base.repo  http://mirrors.aliyun.com/repo/Centos-7.repo`
    - 清除缓存：`yum clean all`
    - 把yum源缓存到本地，加快软件的搜索和安装速度：`yum makecache`
    - 列出 yum 安装包：`yum list`

- yum 安装 MySQL https://www.cnblogs.com/wishwzp/p/7113403.html

    - 安装 wget：`yum -y install wget`
    - 下载安装包：`wget https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm`
    - 安装yum源：`yum -y localinstall mysql57-community-release-el7-11.noarch.rpm `
    - 在线安装：`yum -y install mysql-community-server`
    - 启动服务：`systemctl start mysqld`
    - 设置开机启动：`systemctl enable mysqld`、`systemctl daemon-reload`
    - 获取临时密码：`vi /var/log/mysqld.log`，"A temporary password"后有临时密码
    - 命令行登录：`mysql -u root -p`
    - 修改密码：`ALTER USER 'root'@'localhost' IDENTIFIED BY 'newPassWord';`
    - 设置允许远程登录：`GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'newPassWord' WITH GRANT OPTION;`
    - 退出：`exit;`
    - 防火墙开启3306端口远程访问
        - `firewall-cmd --zone=public --add-port=3306/tcp --permanent`
        - `firewall-cmd --reload`
    - 设置编码
        - `vim /etc/my.cnf`
        - 在[mysqld]下增加：`character_set_server=utf8`
        - 在[client]下增加：`default-character-set=utf8`
    - 重启mysql服务：`systemctl restart mysqld`

- yum 安装 jdk，配置环境变量
    1. 查看系统自带的 jdk 是否已安装：`yum list installed |grep java`
    - 查看yum库中的Java安装包：`yum -y list java*`
    - 将java-1.8.0的所有相关Java程序都安装上：`yum -y install java-1.8.0-openjdk*`
    - 查看 java 版本：`java -version`
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

- 查看 java 进程：`ps -ef | grep java`

- 强制杀死进程：`kill -s 9 进程号`

- 安装终端浏览器 w3m：`yum -y install w3m w3m-img`

- 上传下载文件
```
yum -y install lrzsz
# 下载
sz filename
# 上传
rz
```
- 配置 python3 环境
    - 安装 python3

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


- 安装node

  ```
  sudo yum install epel-release
  sudo yum install nodejs
  sudo yum install npm
  ```

- nginx搭建

  - 安装：`yum -y install nginx`
  - 启动：`service nginx start`
  - 停止：`service nginx stop`
  - 重启：`service nginx restart`
  - 卸载：`yum remove nginx`
  - 查看配置文件nginx.conf路径
    - `ps aux/grep nginx`：查看nginx的路径 param_url
    - `param_url -t`：查看配置文件路径，successful的即是

- nginx配置

  - 若是使用root新建的目录，则目录在`/root`下，在nginx中配置根目录中记得添加`/root`这一级
  - nginx直接访问`/root`目录下的文件会报错 403，可以将文件移动到`/data`下

---

> ##### Q：报错`vim: command not found`

- 参考：http://blog.51cto.com/linushai/1154871
- 输入命令`rpm -qa|grep vim`，如果 vim 已经正确安装，则会返回`vim-minimal`、`vim-common`、`vim-enhanced`三个的信息，缺少哪个安哪个，如`yum -y install vim-enhanced `

> ##### Q：ip能ping通，访问80端口提示`This site can’t be reached.……refused to connect.`

R：centos7.3自带firewall防火墙，防火墙把80端口禁掉了

A：https://www.wordpressleaf.com/2016_1402.html
- 查看防火墙版本：`firewall-cmd --version`
- 查看防火墙运行状态：`firewall-cmd --state`
- 在防火墙中添加80端口权限：`firewall-cmd --zone=public --add-port=80/tcp --permanent`
- 重启防火墙：`systemctl restart firewalld`