# MySQL学习笔记

- ### 数据操纵语言 DML
    1. 不存在记录则插入数据
    ```sql
    insert into deviceentry (customerId,allNumber) select 'c','d'   
    where not exists (select * from deviceentry);  
    ```
    - 多关键字查询
    ```sql
    select * from 表名 where concat(字段1, '分隔符', 字段2, '分隔符', ...字段n) like '%关键字1%' and concat(字段1, '分隔符', 字段2, '分隔符', ...字段n) like '%关键字2%' ......;
    ```

- ### 数据定义语言 DDL


- ### 数据控制语言 DCL
    1. 查看最大连接数
    ```sql
    show variables like "max_connections";
    ```
    - 设置最大连接数
    ```sql
    set global max_connections = 1000;
    ```
    - 设置GROUP_CONCAT()查询结果长度
    ```sql
    SET SESSION group_concat_max_len = 10240;
    ```
    java中：
    ```java
    // 每次的查询之前都需要设置
    jdbcTemplat.execute("SET SESSION group_concat_max_len = 10240")
    ```


- ### 事物控制语言 TCL

---

## 常用函数

- `CONCAT_WS(separator,str1,str2,…)`：用指定分隔符连接字符串