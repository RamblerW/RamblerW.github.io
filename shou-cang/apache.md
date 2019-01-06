# 从0开始python后端开发_配置apache服务器（Mac系统）

> 原文：https://blog.csdn.net/bjbz_cxy/article/details/79299066

首先安装 Homebrew，正确的安装了brew后，那么我们就可以使用brew很轻而易举的安装apache。
只需要在命令行输入
在brew的软件包里apache是httpd后面的24则是版本号，意思就是下载2.4版本的apache服务器
```
# brew install httpd24
```
brew会帮我们自动下载以及安装！
下载完成之后，第一步就是检查是否正确的安装！
在命令行输入：
```
# httpd -v
```
查看httpd信息
示列：
```
# httpd -v
Server version: Apache/2.4.29 (Unix)
Server built:   Dec 28 2017 00:52:51
```
如上所示，正确的输出了Apache服务器的版本号以及所使用的系统内核，就代表Apache服务器已经正确的安装到mac系统上了！
下面开始配置Apache服务器的配置文件
Apache服务器的默认安装目录是/usr/local/etc/httpd
```
# cd /usr/local/etc/httpd
```
然后输入ls查看一下目录文件：
```
# ls
httpd.conf	magic		original
extra		mime.types

```
httpd.conf就是我们要配置的文件，其他文件暂时我们无需了解！
注意在用户组根目录下操作需要root权限，我们要对该文件使用vim编辑器进行编辑，不能直接vim httpd.conf 需要在前面加上sudo
```
sudo vim httpd.conf
```
然后输入root密码
完成上述一系列操作之后开始接下来的文件配置
进入vim编辑界面后使用查找命令查找"Directory"关键字
```
<Directory "/var/www/cgi-bin">
   AllowOverride None
   Order allow,deny
</Directory>
```
配置文件中会有多个"Directory"关键字，我们只要找到类似于上面这样的格式的Directory关键字即可
Directory后面用双引号扩起来的字段是HTTP执行的默认预CGI程序目录
我们将其修改为我们自己的目录即可
这里我就不做修改，我默认目录就是var/www/cgi-bin
然后在下面把
```
AllowOverride None
   Order allow,deny
```
更换为
```
AllowOverride None
   Options +ExecCGI
   Order allow,deny
   Allow from all
```
使阿帕奇支持所有可执行文件并获得该目录下的所有权限
然后继续搜索"LoadModule"关键字，会有多个，我们只需要找到这种书写格式的即可：
```
LoadModule cgi_module lib/httpd/modules/mod_cgi.so
```
找到了如果被“#”注释掉了将#去掉，使其能正常加载cig动态库
在搜索“AddHandler”关键字，可能会有多个，只需要找到这种书写格式即可：
```
AddHandler cgi-script .cgi
```
这个关键字是告诉apache支持那些文件格式！
在.cgi后面加上一个空格和".py"即可让apache服务器支持py文件
```
AddHandler cgi-script .cgi .py
```
然后在搜索关键字“ServerName”，可能会有多个，只需要找到这种书写格式即可：
```
ServerName www.example.com:8080
```
ServerName指令设置了服务器用于辨识自己的主机名和端口号。就是说它后面的值是机器自己的主机名，可以带端口号。这主要用于创建重定向URL。比如，一个放置web服务器的主机名为simple.example.com ，但同时有一个DNS别名www.example.com 。而您希望web服务器更显著一点，可以使用如下的指令：
```
ServerName www.example.com:80
```
当没有指定ServerName时，服务器会尝试对IP地址进行反向查询来推断主机名。如果在ServerName中没有指定端口号，服务器会使用接受请求的那个端口。为了加强可靠性和可预测性，应该使用ServerName显式的指定一个主机名和端口号。
```
ServerName localhost:8080
```
改好之后保存退出vim编辑器
重启apache服务器
```
#sudo httpd -k restart
```
在浏览器里输入：
```
http://localhost:8080
```
如果出现“IS OK”的字样代表apache已经正确的配置，并正常运行。
默认的情况下不在端口号后面加任何路径会默认执行
配置文件中"DrectoryIndex"关键字后方的文件
配置文件中"Drectorylndex"关键字：

```
<IfMoule dir_module>
 
Drectorylndex index.html
 
</IfMoule>
```
你也可以将“Drectorylndex”后面的字段改成你的文件名
index.html是在/var/www文件目录下的，该目录为apache默认文件目录，我们的程序目录在/var/www/cgi-bin目录下，所以如果要使用我们的文件需要加上/cgi-bin/file_name
配置完成之后我们在/var/www/cgi-bin/目录下创建一个python文件
```
sudo vim hello_apache.py
```
注意用户目录下需要root权限一定要加上sudo否则没办法保存
写入如下代码做测试
```
#!/usr/bin/python
# -*- coding: UTF-8 -*-
 
print "Content-type:text/html"
print                               # 空行，告诉服务器结束头部
print '<html>'
print '<head>'
print '<meta charset="utf-8">'
print '<title>Hello Word</title>'
print '</head>'
print '<body>'
print '<h2>Hello World! </h2>'
print '</body>'
print '</html>'
```
写完之后保存，并在命令行中给予运行权限：
```
sudo chmod 755 hello_apache.py
```
或者也可以直接给该文件目录下权限
```
sudo chmod 755 /var/www/cgi-bin
```
这样每次编写新的python文件就不需要重复给予运行权限！
如果不给予运行权限apache会直接将文件内容显示出来，而不执行python脚本！
最后在浏览器中输入
```
http://localhost:8080/cgi-bin/hello_apache.py
```
浏览器的页面标题会变成：Hello Word
页面内容会变成：Hello Word!
如果要想修改域名地址要修改mac系统下的hosts文件
在命令行输入：
进入用户根目录
```
#cd //
```
进入etc目录
```
#cd etc
```
打开hosts文件
```
#sudo vim hosts
```
在最下面输入：
```
test 127.0.0.1
```
然后在浏览器输入test:8080即可
域名可以修改端口号也一样可以修改
进入apache配置目录
```
#cd /usr/local/etc/httpd
```
打开配置文件
```
#sudo vim httpd.conf
```
使用vim查找命令查找
```
Listen 8080
```
将后面的8080改成你想要的任意端口号，注意要保证该端口号没用被占用
```
Listen 8081
```
保存退出，重启apache，在浏览器地址栏输入：
```
test:8081
```
即可跳转到我们指定的默认的html文件下！