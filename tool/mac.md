> ### 操作

1. 改变Launchpad应用图标大小
   改为6行8列
   ```
   defaults write com.apple.dock springboard-rows -int 6
   defaults write com.apple.dock springboard-columns -int 8
   killall Dock
   ```

   killall Dock
   恢复默认
   ```
   defaults write com.apple.dock springboard-rows Default
   defaults write com.apple.dock springboard-columns Default
   killall Dock
   ```

2. 添加环境变量
   ```
   open -e .bash_profile
   export PATH=${PATH}:/Library/Android/sdk/platform-tools
   source .bash_profile
   ```

3. 查看软件安装位置
   ```
   which software_name
   ```

4. 显示当前所在目录
   ```
   pwd
   ```

5. 允许从任何来源安装应用程序
   ```
   sudo spctl --master-disable
   ```

6. 给指定目录sudo权限

   ```
   sudo chown -R sudo权限用户名 目录
   ```

7. 隐藏桌面所有内容

   ```
   defaults write com.apple.finder CreateDesktop -bool FALSE; killall Finder
   ```

8. 显示桌面所有内容

   ```
   defaults write com.apple.finder CreateDesktop -bool true; killall Finder
   ```

9. 1

> ### 系统快捷键

1. 苹果logo：option + shift + K
2. emoji表情：ctrl + cmd + space
3. 自动操作：cmd + shift + option + S
4. 移动文件：cmd + option + V
5. 切输入法：ctrl + option + space
6. 打开finder：option + cmd + space
7. 打开终端：cmd + shift + T（自定义）
8. 终端清屏：cmd + K
9. 锁屏：cmd + shift + L（自定义）
10. 强制退出：cmd + option + shift + Esc
11. Finder中跳转至指定路径：cmd + shift + G
12. 锁屏：ctrl + shift + power
13. Home/End：cmd + ↑/↓/←/→
14. 打开新页签：cmd + T
15. 关闭当前标签页：cmd + W
16. 屏幕取词：cmd + ctrl + D
17. 搜索后打开文件所在目录：cmd + enter

> ### Mac软件

[[http://www.chinamac.cc/](http://www.chinamac.cc/)    apple / 20181818

[https://www.jianshu.com/p/235efc09d647](https://www.jianshu.com/p/235efc09d647)

**iWork**：App Store

卸载软件**AppCleaner**：[http://freemacsoft.net/appcleaner/](http://freemacsoft.net/appcleaner/)

解压缩软件**The Unarchiver**：[https://theunarchiver.com/](https://theunarchiver.com/)

思维导图软件**MindNode**：[https://mindnode.com/](https://mindnode.com/)

IINA

CheatSheet 查看快捷方式

Hombrew    开源软件

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

1. **安装MySQL**
   1. 安装完成后，进入/usr/local/mysql/bin，查看此目录下是否有mysql，执行vim ~/.bash\_profile，在该文件中添加mysql/bin的目录：PATH=$PATH:/usr/local/mysql/bin，添加完成后，输入冒号:，然后输入wq保存，最后在命令行输入source ~/.bash\_profile
   2. 登录mysql：`mysql -uroot -p`
   3. 修改密码：
      ```
      SET PASSWORD FOR 'root'@'localhost' = PASSWORD('newpass');
      ```

2. **安装下载器you-get和视频合并工具ffmpeg**
   ```
   brew install you-get
   brew install ffmpeg
   ```

   下载步骤：
   ```
   you-get -i https://www.bilibili.com/video/av5434702/
   you-get --format=hdmp4 'https://www.bilibili.com/video/av5434702/'
   ```

3. **安装Tomcat**  
   1. 解压Tomcat到目录  
   2. sudo chmod 755 /Library/Tomcat/bin/\*.sh  
   3. sudo sh startup.sh

4. **安装python服务器 Apache**

   [python \| 从0开始python后端开发\_配置apache服务器（Mac系统）](shou-cang/apache.md)

5. **Python**

   - 使用 tesseract：`brew install tesseract`

6. 1




