> ##### Q：javaWeb登录时报错：`java.lang.SecurityException: JCE cannot authenticate the provider BC`

A：

1. 在 Macintosh HD/Library/Java/JavaVirtualMachines/jdk1.8.0_151.jdk/Contents/Home/jre/lib/security/java.security添加代码：`security.provider.9=org.bouncycastle.jce.provider.BouncyCastleProvider`，这里的9，根据前面的代码编号递增
2. 添加2个扩展包到jre/lib/ext目录下：bcprov-jdk15-136.jar     bcprov-jdk16-146.jar