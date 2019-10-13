

---

> ##### Q. 报错<font color=red>Caused by: java.lang.IllegalArgumentException: Could not resolve resource location pattern [classpath:com/qinkangdeid/mapping/*.xml]: class path resource [com/qinkangdeid/mapping/] cannot be resolved to URL because it does not exist</font>

R：`classpath:com/qinkangdeid/mapping/*.xml`的`classpath`后加一个`*`

A：（参考资料：https://blog.csdn.net/qinkang1993/article/details/57626434）