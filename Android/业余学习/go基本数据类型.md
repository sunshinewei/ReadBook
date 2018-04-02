###   基本数据类型



##### 整型int 和浮点型float

在格式化字符串里，%d 用于格式化整数（%x 和 %X 用于格式化 16 进制表示的数字），%g 用于格式化浮点型（%f 输出浮点数，%e 输出科学计数表示法），%0d 用于规定输出定长的整数，其中开头的数字 0 是必须的。

%n.mg 用于表示数字 n 并精确到小数点后 m 位，除了使用 g 之外，还可以使用 e 或者 f，例如：使用格式化字符串 %5.2e 来输出 3.4 的结果为 3.40e+00。

:= 是声明并赋值，并且系统自动推断类型，不需要var关键字



##### 时间和日期（Time）


##### switch与java不同，可以是任何数据类型



##### for-range结构

<pre>
for pos, char := range str {
...
}
</pre>


##### 标签与goto
标签的使用

<pre>
LABEL1:
    for i := 0; i <= 5; i++ {
        for j := 0; j <= 5; j++ {
            if j == 4 {
                continue LABEL1
            }
            fmt.Printf("i is: %d, and j is: %d\n", i, j)
        }
    }
</pre>

goto的使用：


如果您必须使用 goto，应当只使用正序的标签（标签位于 goto 语句之后），但注意标签和 goto 语句之间不能出现定义新变量的语句，否则会导致编译失败。


##### 函数

函数可以多值返回

<pre>
num1, num2 = add(2, 4)

func add(a int, b int) (int, int) {

	return a * 3, b * 4

}
</pre>

##### 空白符：

空白符用来匹配一些不需要的值，然后丢弃掉。

##### 可以传递变长参数
如果函数的最后一个参数是采用 ...type 的形式，那么这个函数就可以处理一个变长的参数，这个长度可以为 0，这样的函数称为变参函数。

#####  defer和追踪（log库）
关键字 defer 允许我们推迟到函数返回之前一刻才执行某个语句或函数。

实例如下：（执行结果先执行输出语句，在执行方法体）
<pre>
defer funSwitch()

fmt.Println("输出结果为num1=%d,num2=%d", num1, num2)
</pre>

##### 切片
是对数组一个连续片段的引用.对数组的抽象。与数组相比切片的长度不固定，可以追加元素，再追加时，可能使贴片的容量增大。
对于切片来说，不需要说明长度。
可以使用<code>make</code>创建切片
<pre>
 var numbers = make([]int,3,5)
</pre>

##### Range关键字
Go 语言中 range 关键字用于for循环中迭代数组(array)、切片(slice)、通道(channel)或集合(map)的元素。在数组和切片中它返回元素的索引值，在集合中返回 key-value 对的 key 值。
<pre>
numbers := []int{3, 6, 8, 6, 5, 9}

	for _, nums := range numbers {

		fmt.Print(nums)
	}
</pre>

##### Map关键字
构建map的两种方法
<pre>
/* 声明变量，默认 map 是 nil */
var map_variable map[key_data_type]value_data_type

/* 使用 make 函数 */
map_variable := make(map[key_data_type]value_data_type)
</pre>

使用Map
<pre>
var maps map[string]string

	maps = make(map[string]string)//创建集合，不然map集合为空

	maps["x"] = "aaa"

	maps["y"] = "bbb"

	maps["z"] = "ccc"

	for str := range maps {

		fmt.Println(str, "  "+maps[str])
	}
</pre>


##### 接口



