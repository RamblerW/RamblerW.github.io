> MySQL

1. 数据库默认编码为_latin1_

   解决方案：

   - 复制配置文件 _my.cnf_ 至 _etc_ 文件夹下，并添加如下配置

     ```
     [client]
     default-character-set = utf8
     [mysqld]
     character-set-server = utf8
     ```

   - 重启MySQL服务，执行命令```SHOW VARIABLES LIKE 'character%'```查看编码

2. 111