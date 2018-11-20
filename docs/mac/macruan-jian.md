# 快捷键 & 操作 & 软件安装

http://www.chinamac.cc/	apple / 20181818
https://www.jianshu.com/p/235efc09d647
**iWork**：App Store
卸载软件**AppCleaner**：http://freemacsoft.net/appcleaner/
解压缩软件**The Unarchiver**：https://theunarchiver.com/
思维导图软件**MindNode**：https://mindnode.com/
IINA 
CheatSheet 查看快捷方式

Hombrew	开源软件
```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

1. **安装MySQL**
  1. 安装完成后，进入/usr/local/mysql/bin，查看此目录下是否有mysql，执行vim ~/.bash_profile，在该文件中添加mysql/bin的目录：PATH=$PATH:/usr/local/mysql/bin，添加完成后，输入冒号:，然后输入wq保存，最后在命令行输入source ~/.bash_profile
  2. 登录mysql：```mysql -uroot -p```
  3. 修改密码：
  ```
  SET PASSWORD FOR 'root'@'localhost' = PASSWORD('newpass');
  ```
- **安装下载器you-get和视频合并工具ffmpeg**
```
brew install you-get
brew install ffmpeg
```
下载步骤：
```
you-get -i https://www.bilibili.com/video/av5434702/
you-get --format=hdmp4 'https://www.bilibili.com/video/av5434702/'
```
- **安装Tomcat**
  1. 解压Tomcat到目录
  2. sudo chmod 755 /Library/Tomcat/bin/*.sh
  3. sudo sh startup.sh