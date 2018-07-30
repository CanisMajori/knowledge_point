

## sql语句

用引号引起来，换行的话用反引号



# 查：

```SQL
SELECT 字段1，字段2, FROM 表 WHERE 字段1=?`//?用来在qux.query()中传值   
```

追加语句前要加空格

```sql
SELECT id,name,salary FROM employee WHERE 1；
 AND name="'+name+'" '；//追加数据
 ORDER BY salary DESC //以salary降序排列
 ORDER BY salary  ASC|DESC, id DESC;//可以多个条件同时
```

模糊查询

```sql
sql+='  AND kw LIKE "%'+ kw+'%"'
```

%  关键词%：查询包含关键词的

%  关键词：查询以关键词结尾的

  关键词%：查询以关键词开头的

指定查询范围

```sql
SELECT  *  FROM  表  WHERE 判断条件 ORDER BY id 
		LIMIT start, num//     表中id从 start开始  查询num个

```

分组查询：

​       GROUP  BY 字段1：按照指定的字段分组查询；

判断条件：

​       =、<、>、>=、<=、<>(不等于)、

AND、OR、NOT

LIKE、IN、BETWEEN

NOT LIKE、NOT IN

```sql
select *  FROM  表 WHERE 字段 between 7 AND 18//在id7到18中
```

使用中文排序

对字段进行代码转换：

```sql
SELECT  *  FROM 表 ORDER  BY CONVERT(字段 USING GBK)
```



# 增：

```sql
INSERT INTO reg(username,password,sex,email,tel,regtimes) value(?,?,?,?,?,?) //reg：表的名字
```

# 删：

```sql
DELETE FROM 表 WHERE id = ? LIMIT 1  
```

//从表中删除符合id=？的值，限制只删除一个

#### 风险规避：

- 前端删除前 确认
- 加上limit
- 数据备份
- 回收站
- 删除操作只改变 delstatus字段的值  1表示删除状态

# 改

```sql
UPDATE 表名 SET 字段1=new1,2,3  WHERE 判断条件
```



DOS窗口操作数据库：

```sql
mysql -hlocalhost -uroot -p//登录数据库：

set password='新密码'；//登录数据库：
```

# 多表查询

### 左连接：

```sql
SELECT  q.qtitle, q.qanswer, c.qname
FROM  questions AS q 
LEFT JOIN qclass AS c 
ON q.qcid = c.qcid 
WHERE c.qcid = 2 AND q.qtitle LIKE '%变量%'
//左连接时 左边 主表的记录不能是null
```

### 右连接：

```sql
SELECT  q.qtitle, q.qanswer, c.qname
FROM  questions AS q
RIGHT JOIN qclass AS c
ON q.qcid = c.qcid //在q,c 的qcid相等时
//右连接时 右边 主表的记录不能是null
```

### 内连接：

```sql
SELECT  q.qtitle, q.qanswer, c.qname
FROM  questions AS q 
INNER JOIN qclass AS c 
ON q.qcid = c.qcid
//两边都不能为null
```



# 非常多的表的查询

```sql
SELECT  u.username, u.passwd, p.name, c.name, a.name
FROM  user  AS u
LEFT JOIN province  AS p ON u.pid = p.pid  
LEFT JOIN city  AS c ON u.cid = c.cid  
LEFT JOIN area  AS a ON u.aid = a.aid 
WHERE  c.cid = 10 AND a.aid = 20 AND u.username LIKE ‘模糊查询%’

```

 



#### 一些常用函数：

​	平均数：AVG

   	总数：SUM

   	最大值：MAX

​	最小值：MIN