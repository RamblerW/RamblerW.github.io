# 解决Intellij idea Java JDK多重选择提示问题
原文：https://blog.csdn.net/ruglcc/article/details/72627254

> ### 问题引出

当前我们对idea 写Java的程序进行编译时，会报如下的错误提示，原因在于 idea 检测到了两个位置有jdk，它不知道选哪一个，就随便选了一个。

objc[63766]: Class JavaLaunchHelper is implemented in both /Library/Java/JavaVirtualMachines/jdk1.8.0_111.jdk/Contents/Home/bin/java (0x10390d4c0) and /Library/Java/JavaVirtualMachines/jdk1.8.0_111.jdk/Contents/Home/jre/lib/libinstrument.dylib (0x1039e94e0). One of the two will be used. Which one is undefined.

> ### 问题解决

#### 首先配置好环境变量
以Mac为例
编辑 .bash_profile 文件， 在最后添加
```
JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_111.jdk/Contents/Home
CLASSPAHT=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
PATH=$JAVA_HOME/bin:$PATH:
export JAVA_HOME
export CLASSPATH
export PATH
```
最后别忘记让这个配置生效, 在终端执行
```
source .bash_profile
```
#### 配置Intellij Idea
1. ####打开idea.properties文件
```
help->edit custom properties
```
- ####在文件中添加一行
```
idea.no.launcher=true
```
- ####重启 idea 问题解决