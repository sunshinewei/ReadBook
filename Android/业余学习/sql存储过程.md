### 存储过程
<pre><code>
DELIMITER   //
 CREATE PROCEDURE GetAllProducts()
   BEGIN
   SELECT *  FROM products;
   END  //
DELIMITER   ;
</code></pre>

#### 存储过程的变量：
变量的申明：<code>DECLARE</code>
<pre><code>
DECLARE variable_name datatype(size) DEFAULT default_value;
</code></pre>

#### 为变量赋值
<pre><code>
SET  variable_name=10;
</code></pre>
####  存储过程的参数形式
<code>IN</code>
<code>OUT</code>
<code>INOUT</code>

#### if语句

<pre><code>
IF expression THEN 
   statements;
ELSE
   statements;
END IF;
如果表达式(expression)计算结果为TRUE，那么将执行statements语句，否则控制流将传递到END IF之后的下一个语句。
</code></pre>

#### 存储函数

<pre><code>
CREATE FUNCTION function_name(param1,param2,…)
    RETURNS datatype
   [NOT] DETERMINISTIC
 statements
</code></pre>

#### 创建触发器
<pre><code>
CREATE TRIGGER trigger_name trigger_time(before/after) trigger_event(insert/updata/delete)
 ON table_name
 FOR EACH ROW
 BEGIN
 ...
 END;
</code></pre>


#### MySql的用户创建

<pre><code>
CREATE USER dbadmin@192.168.1.100 
IDENTIFIED BY 'pwd123';
</code></pre>
