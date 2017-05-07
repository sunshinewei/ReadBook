### JavaScript的基本知识

#### 注释
1.通过//进行单行注释。
2./*   */进行多行注释。

#### 数据类型
JavaScript提供七种不同的data types(数据类型)，它们是undefined（未定义）, null（空）, boolean（布尔型）, string（字符串）, symbol(符号), number（数字）, and object（对象）。
在javascript中声明一个变量通过
```
var a;
```

Variable （变量）的名字可以由数字、字母、$ 或者 _组成，但是不能包含空格或者以数字为首。

当 JavaScript 中的变量被声明的时候，程序内部会给它一个初始值 undefined。当你对一个值为 undefined 的变量进行运算操作的时候，算出来的结果将会是 NaN，NaN 的意思是 "Not a Number"。当你用一个没有 定义 的变量来做字符串连接操作的时候，它会如实的输出"undefined"。

#### 变量的命名规则
在 JavaScript 中所有的变量都是大小写敏感的。这意味着你要区别对待大写字母和小写字母。

使用 驼峰命名法 来书写一个 Javascript 变量，在 驼峰命名法 中，变量名的第一个单词的首写字母小写，后面的单词的第一个字母大写。
