#### 变量的生命

var：可变变量，可以通过重新分配来改为另一个值的变量。<p>
val:只读变量，这种声明变量的方式相当于java中的final变量。一个val创建的时候必须初始化，因为以后不能被改变。


#### When表达式
When的存在取代了java中的switch:<p>
如：
<pre><code>
when (obj) {
  1          -> "One"
  "Hello"    -> "Greeting"
  is Long    -> "Long"
  !is String -> "Not a string"
  else       -> "Unknown"
}
</code></pre>
同时也可以使用in操作符检查集合是否包含某个对象
<pre><code>
val items = setOf("apple", "banana", "kiwi")
  when {
    "orange" in items -> println("juicy")
    "apple" in items -> println("apple is fine too")
  }
</code></pre>

#### Unit
如果函数返回 Unit ，返回类型应该省略。

#### 扩展
##### 函数扩展：

##### 属性扩展：