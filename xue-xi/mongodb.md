> 面向文档的数据库

- 启动服务：`mongod`（默认访问地址：http://localhost:27017）

- shell连接服务：`mongodb://localhost`

- 连接命令：`mongodb://username:password@hostname/dbname`

- 进入命令行客户端：`mongo`

- 显示所有数据列表：`show dbs`

- 显示当前数据库对象或集合：`db`

- 创建数据库 \ 连接到指定的数据库：`use 数据库名`（新建的数据库需要插入数据才能看到）

- 删除数据库：切换到要删除的数据库，然后 `db.dropDatabase()`

- 删除集合：`db.collection.drop()

- MongoDB概念解析：

| sql术语/概念 | MongoDB术语/概念 | 解释/说明                                   |
| ------------ | :--------------- | ------------------------------------------- |
| database     | database         | 数据库                                      |
| table        | collection       | 数据库表/集合                               |
| row          | document         | 数据记录行/文档                             |
| column       | field            | 数据字段/域                                 |
| index        | index            | 索引                                        |
| table joins  |                  | 表连接，mongoDB不支持                       |
| primary key  | primary key      | 主键，mongoDB自动将 **\_id** 字段设置为主键 |

- 数据库名命名规则
  - 不能是空字符串
  - 不能含有空格、.、$、/、\和\0（空字符）
  - 应==全部小写==
  - 最多64字节

- 特殊的数据库
  - **admin**：root权限的数据库
  - **local**：永远不会被复制，可以用来存储限于本地单台服务器的任意集合
  - **config**：用于保存分片的相关信息

- 文档：一个键值对，即BSON
  - ==MongoDB 区分类型和大小写==
  - 键不能重复

- 集合：MongoDB 文档组
  - 集合名不能以`system.`开头，这是为系统集合保留的前缀
  - Capped collections：固定大小的集合

- 数据类型

| 数据类型           | 描述                                                       |
| ------------------ | ---------------------------------------------------------- |
| String             | 字符串，UTF8编码的才是合法的                               |
| Integer            | 整型数值                                                   |
| Boolean            | 布尔值                                                     |
| Double             | 双精度浮点数                                               |
| Min/Max keys       | 将一个值与BSON元素的最低值和最高值相比较                   |
| Arrays             | 用于将数组或列表或多个值存储为一个键                       |
| Timestamp          | 时间戳                                                     |
| Object             | 用于内嵌文档                                               |
| Null               | 空值                                                       |
| Symbol             | 符号。基本等同于字符串类型，一般用于采用特殊符号类型的语言 |
| Date               | 日期时间，用UNIX时间格式存储                               |
| Object ID          | 对象ID，用于创建文档的ID                                   |
| Binary Data        | 二进制数据                                                 |
| Code               | 代码类型                                                   |
| Regular expression | 正则表达式类型                                             |

- 插入操作（不存在会自动创建）
  - `db.表名.insert({'key1':'value1','key2':'value2'})`
  - `db.表名.save({'key1':'value1','key2':'value2'})`：指定 _id 为更新，不指定为插入

- 更新操作：`db.表名.update(criteria, objNew, upsert=false, multi=false)`
  - **criteria**：update查询条件，类似于sql update中的where
  - **objNew**：update对象和更新操作符等，类似于sql update中的set
  - **upsert**：若不存在update的记录，则插入 objNew
  - **multi**：false - 只更新找到的第一条数据；true - 更新找到的所有数据

- 删除操作：`db.表名.remove(query, justOne, writeConcern)`
  - **query**：（可选）删除的文档的条件
  - **justOne**：（可选）如果设为 true 或 1，则只删除一个文档
  - **writeConcern**：（可选）抛出异常的级别

- 查询操作：
  - `db.表名.find(query, projection)`：以非结构化的方式显示

    - **query**：（可选）查询条件
    - **projection**：（可选）使用投影操作符返回键值为1或true的键，_id 默认显示

  - `db.表名.find().pretty()`：以格式化的方式显示

  - mongoDB 与 RDBMS Where 比较

    | 操作     | 格式                       |
    | -------- | -------------------------- |
    | 等于     | `{<key>: <value>}`         |
    | 小于     | `{<key>: {$lt: <value>}}`  |
    | 小于等于 | `{<key>: {$lte: <value>}}` |
    | 大于     | `{<key>: {$gt: <value>}}`  |
    | 大于等于 | `{<key>: {$gte: <value>}}` |
    | 不等于   | `{<key>: {$ne: <value>}}`  |

  - OR：`db.表名.find({$or: [{key1: value1}, {key2, value2}]})`

- $type 操作符：基于BSON类型来检索集合中匹配的数据类型，并返回结果。

   | **类型**                | **数字** | **备注**       |
   | ----------------------- | -------- | -------------- |
   | Double                  | 1        |                |
   | String                  | 2        |                |
   | Object                  | 3        |                |
   | Array                   | 4        |                |
   | Binary data             | 5        |                |
   | Undefined               | 6        | 已废弃。       |
   | Object id               | 7        |                |
   | Boolean                 | 8        |                |
   | Date                    | 9        |                |
   | Null                    | 10       |                |
   | Regular Expression      | 11       |                |
   | JavaScript              | 13       |                |
   | Symbol                  | 14       |                |
   | JavaScript (with scope) | 15       |                |
   | 32-bit integer          | 16       |                |
   | Timestamp               | 17       |                |
   | 64-bit integer          | 18       |                |
   | Min key                 | 255      | Query with -1. |
   | Max key                 | 127      |                |

   例：查询 title 为 String 的数据：`db.表名.find({"title" : {$type : 2}})`

- limit()：读取指定数量的数据记录，接受一个数字参数，作为读取的记录条数。

语法：`db.表名.find().limit(NUMBER)`

- skip()：跳过指定数量的数据，接受一个数字参数，作为跳过的记录条数。

语法：`db.表名.find().skip(NUMBER)`

- sort()：通过参数指定排序字段和排序方式，1 为升序排列，-1 为降序排列。

语法：`db.表名.find().sort({KEY:1})`

- 索引
  - 创建索引：`db.表名.ensureIndex({KEY1:1,KEY2:-1})`，KEY 为索引字段，1 为升序，-1 为降序
  - ensureIndex() 可选参数见 https://www.w3cschool.cn/mongodb/mongodb-indexing.html

- 聚合：`db.表名.aggregate()`

- 正则表达式

  语法：`db.表名.find({key:{$regex:"regexExp",$options:"$i"}})`

  说明：`$options`为可选参数，`$options:"$i"`为不区分大小写

---

参考资料：

1. W3CSchool | MongoDB教程：https://www.w3cschool.cn/mongodb/