###  常见操作符
<code>order by</code>:对指定的列进行排序。(默认升序，降序DESC)
<pre><code>
select * from student_table order by name DESC;
</code></pre>

#### Top子句
用于规定要返回的记录的数目

<pre><code>
 select * from student_table limit 3;
</code></pre>

可以这样排序
<pre><code>
 SELECT name FROM Products ORDER BY price * quantity DESC, name ASC limit 1,m;//从第几条开始，m是几条数据
</code></pre>

#### 通配符
<pre><code>
% ：  替代一个或多个字符

— ：代替一个字符
[charlist] ：字符列中的任何单一字符
[^charlist] [!charlist] ：不在字符列中的任何单一字符
</code></pre>

#### 别名 as

#### 截取字符串SUBString(Name,1,3)


#### Union/Union ALL
UNION 操作符用于合并两个或多个 SELECT 语句的结果集。

请注意，UNION 内部的 SELECT 语句必须拥有相同数量的列。列也必须拥有相似的数据类型。同时，每条 SELECT 语句中的列的顺序必须相同。

### 创建索引
<pre><code>
CREATE INDEX index_name
ON table_name (column_name)
不为一列时可以（column1, column2）
</code></pre>

#### Drop语句：删除表，索引，数据库
####  Alter语句：

#### 将数据源导入数据库中
<pre><code>
source D:/worksp/yiibaidb.sql;
</code></pre>
#### 将为null的映射到其他值用if语句：
<pre><code>
select customername,if(state is null,'N/A',state),country from customers;
</code></pre>

#### 常见的函数
field（）:排序指定什么位置
