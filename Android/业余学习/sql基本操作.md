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

#### 通配符
<pre><code>
% ：  替代一个或多个字符

— ：代替一个字符
[charlist] ：字符列中的任何单一字符
[^charlist] [!charlist] ：不在字符列中的任何单一字符
</code></pre>

#### 别名 as


#### Union/Union ALL
UNION 操作符用于合并两个或多个 SELECT 语句的结果集。

请注意，UNION 内部的 SELECT 语句必须拥有相同数量的列。列也必须拥有相似的数据类型。同时，每条 SELECT 语句中的列的顺序必须相同。
