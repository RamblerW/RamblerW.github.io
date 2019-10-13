- 创建数据库：`create database 数据库名 default charset=utf8`
- 不存在记录则插入数据：`insert into deviceentry (customerId,allNumber) select 'c','d'where not exists (select * from deviceentry);  `
- 多关键字查询：`select * from 表名 where concat(字段1, '分隔符', 字段2, '分隔符', ...字段n) like '%关键字1%' and concat(字段1, '分隔符', 字段2, '分隔符', ...字段n) like '%关键字2%' ......;`
- 查看最大连接数：`show variables like "max_connections";`
- 设置最大连接数：`set global max_connections = 1000;`
- 设置GROUP_CONCAT()查询结果长度

  - `SET SESSION group_concat_max_len = 10240;`

  - java中（每次的查询之前都需要设置）：`jdbcTemplat.execute("SET SESSION group_concat_max_len = 10240")`


  - 用指定分隔符连接字符串：`CONCAT_WS(separator,str1,str2,…)`

  - 查看数据库编码：`SHOW VARIABLES LIKE 'character%'`

  - 修改数据库编码（默认编码为_latin1_）


    - 复制配置文件 _my.cnf_ 至 _etc_ 文件夹下，并添加如下配置
    
      ```
      [client]
      default-character-set = utf8
      [mysqld]
      character-set-server = utf8
      ```


