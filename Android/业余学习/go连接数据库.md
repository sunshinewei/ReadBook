### Go连接数据库

#### 常见的关键几个函数
<code>sql.open()</code>:打开一个注册过的数据库驱动
<code>db.Prepare()</code>:函数用来返回准备要执行的sql操作，然后返回准备完毕的执行状态。
<code>db.Query()</code>:函数用来直接执行sql返回的Rows结果。
<code>stmt.Exec()</code>:函数用来执行stmt准备好的sql语句。

### beego连接数据库

