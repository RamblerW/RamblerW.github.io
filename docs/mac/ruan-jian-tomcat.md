# Tomcat

1. 启动：移动到bin目录下，执行`sudo sh startup.sh`
2. 停止：移动到bin目录下，执行`sudo sh shutdown.sh`
3. 运行Tomcat报错：error=13, permission denied
   * 解决方案：打开Terminal，找到catalina.sh所在的文件夹下，输入`chmod a+x catalina.sh`即可
4. 配置SSL
   1. 生成SSL
      ```
      keytool -v -genkey -alias tomcat -keyalg RSA -keystore ~/Desktop/tomcat.keystore
      ```
   2. 将`tomcat.keystore`复制到`tomcat/conf`下
   3. 修改`conf/server.xml`
      ```
      <Connector port="8443" protocol="org.apache.coyote.http11.Http11NioProtocol"
           maxThreads="150" SSLEnabled="true" scheme="https" secure="true"
           clientAuth="false" sslProtocol="TLS" 
           keystoreFile="conf/tomcat.keystore"
           keystorePass="123456"/>
      ```



