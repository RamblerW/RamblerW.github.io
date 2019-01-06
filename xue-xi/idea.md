# IDEA使用笔记（MAC）
### 1. 快捷键
1. 查看接口实现类：cmd + option + B
- 打开Terminal：option + F12
- 复制行：cmd + D
- 删除行：cmd + Y
- 替换：cmd + R
- 向下插入行：shift + enter
- 实现方法：cmd + I
- 上/下移：option + shift + ↑/↓
- 全局查找：ctrl + shift + F
- 大小写转换：cmd + shift + U
- 重写方法：cmd + O

### 2. 常见问题
1. 运行Tomcat报错：error=13, permission denied
    * 解决方案：打开Terminal，找到catalina.sh所在的文件夹下，输入```chmod a+x catalina.sh```即可
    
    
### 3. 功能文档
1. 自动生成Hibernate映射文件及实体类：https://blog.csdn.net/qq_34197553/article/details/77718925