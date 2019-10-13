> ### Chrome

- 快捷键
  - 关闭当前窗口：cmd + W
  - 切换页签：cmd + option + ←/→
  - 开发者工具：cmd +option + i
  - 回到主页：cmd + shift + H

> ### idea使用笔记

- 快捷键（参考：[https://www.cnblogs.com/summer-fate/p/7258442.html](https://www.cnblogs.com/summer-fate/p/7258442.html)）
  - 查看接口实现类：cmd + option + B
  - 打开Terminal：option + F12
  - 复制行：cmd + D
  - 删除行：cmd + Y
  - 替换：cmd + R
  - 工程全局替换：ctrl + shift + R
  - 向下插入行：shift + enter
  - 实现方法：cmd + I
  - 上/下移：option + shift + ↑/↓
  - 全局查找：ctrl + shift + F
  - 大小写转换：cmd + shift + U
  - 重写方法：cmd + O
  - 根据文件名打开文件： cmd + shift + N
  - 把代码包在块里（如try/catch）：cmd + option + T
  - 自动代码（如fori为for循环）：cmd + J
  - 格式化代码：cmd + option + L
  - 返回至上/下次浏览的位置：cmd + option + ←/→
  - 回到方法最前/后面：fn + ↑/↓
  - 回到文件最前/后面：cmd + fn + ←/→
  - 显示最近的文件： cmd + E
  - 定位错误：F2
  - 查看断点：cmd + shift + F8
  - getter/setter：ctrl + enter
  - 添加书签：cmd + F11
  - 查看书签：shift + F11

- 自动生成Hibernate映射文件及实体类：[https://blog.csdn.net/qq\_34197553/article/details/77718925](https://blog.csdn.net/qq_34197553/article/details/77718925)

> ### Sublime

- 快捷键
  - 编辑多行：选中多行，cmd + shift + L
  - 格式化SQL：cmd + K + F
  - 格式化json：ctrl + cmd + J
  - 替换：cmd + option + F
  - 大/小写：cmd + K + U / L
  - 上下移动：ctrl + cmd + ↑ / ↓
  - 复制当前行：cmd + shift + D
  - 选择下一个：cmd + D

> ### Tomcat

- 启动：移动到bin目录下，执行`sudo sh startup.sh`

- 停止：移动到bin目录下，执行`sudo sh shutdown.sh`

- 运行Tomcat报错：<font color=red>error=13, permission denied</font>

  - 解决方案：打开Terminal，找到catalina.sh所在的文件夹下，输入`chmod a+x catalina.sh`即可

- 运行Tomcat报错：<font color=red>ContainerBase.addChild: start: org.apache.catalina.LifecycleException: Failed to start component [StandardEngine[Catalina].StandardHost[localhost].StandardContext</font>

  - 解决方案：在Tomcat配置文件/conf/catalina.properties中在`tomcat.util.scan.StandardJarScanFilter.jarsToSkip=`后添加`*.jar`
  - 参考：https://blog.csdn.net/hf_programmer/article/details/79085682

- 配置SSL

  - 生成SSL：`keytool -v -genkey -alias tomcat -keyalg RSA -keystore ~/Desktop/tomcat.keystore`

  - 将`tomcat.keystore`复制到`tomcat/conf`下

  - 修改`conf/server.xml`

    ```
    <Connector port="8443" protocol="org.apache.coyote.http11.Http11NioProtocol"
         maxThreads="150" SSLEnabled="true" scheme="https" secure="true"
         clientAuth="false" sslProtocol="TLS" 
         keystoreFile="conf/tomcat.keystore"
         keystorePass="123456"/>
    ```

- 111



