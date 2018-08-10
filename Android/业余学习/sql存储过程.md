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