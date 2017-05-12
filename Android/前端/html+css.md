### 总结
#### 样式
内联样式和外连样式

#### id 和 class选择器

使用 id 属性有若干好处，一旦当你开始使用 jQuery 的时候你会有更深的体会。

id 属性应该是唯一的，虽然浏览器并不强制唯一，但基于最佳实践，这一点是被广泛认可的，所以请不要给一个以上的元素设置相同的 id 属性。

然而，在 <style> 部分中 class 声明的顺序却非常重要，第二个声明总是比第一个具有优先权。因为 .blue-text 是第二个声明，它覆盖了 .pink-text 属性。

你声明的这个 CSS 在 pink-text类选择器的上面还是下面是无所谓的，因为 id 属性总是具有更高的优先级。

行内样式将覆盖style 中定义的所有 CSS。

很多情况下，你会使用 CSS 库，这些库可能会意外覆盖掉你自己的 CSS。所以当你需要确保某元素具有指定的 CSS 时，你可以使用 !important。
如：

<pre>
.pink-text {
    color: pink !important;
  }
</pre>
#### a元素
也叫anchor（锚点）元素，既可以用来链接到外部地址实现页面跳转功能，也可以链接到当前页面的某部分实现内部导航功能。

使用方式：
<pre>
<p>Here's a <a href="http://freecodecamp.cn"> link to FreeCodeCamp中文社区 </a> for you to follow.</p>
</pre>
有时你想为你的网站添加一个a元素，但此时你还不知道要将它们链接到哪儿，此时可以使用固定链接。
把你的a元素的href属性的值替换为一个#，别名hash(哈希)符号，将其变为一个固定链接。
####alt属性
也被称为alt text, 是当图片无法加载时显示的替代文本。alt属性对于盲人或视觉损伤的用户理解一幅图片中所描绘的内容非常重要，搜索引擎也会搜索alt属性。

简而言之，每一张图片都应该有一个alt属性！

你可以像下面例子中一样为img元素添加一个alt属性：

<pre>
<img src="www.your-image-source.com/your-image.jpg" alt="your alt text">
</pre>

#### 表单设置
当你设计表单时，你可以指定某些选项为必填项(required)，只有当用户填写了该选项后，用户才能够提交表单。

使用方法：

<pre>
<input type="text" required>
</pre>

##### 单选与多选

多选一的场景就用radio button(单选按钮)

单选按钮只是input输入框的一种类型。

每一个单选按钮都应该嵌套在它自己的label(标签)元素中。
<pre>
 <label><input type="radio" name="indoor-outdoor"> Indoor</label>
</pre>

注意：所有关联的单选按钮应该使用相同的name属性。

复选按钮是input的输入框的另一种类型。

每一个复选按钮都应该嵌套进label元素中。

所有关联的复选按钮应该具有相同的name属性。

下面是复选按钮的例子：
<pre>
<label><input type="checkbox" name="personality"> Loving</label>
</pre>

使用checked属性，你可以设置复选按钮和单选按钮默认被选中。

为此，只需在input元素中添加属性checked

如：
<pre>
    <input type="radio" name="test-name" checked>
</pre>

#### div元素
也被称作division(层)元素，是一个盛装其他元素的通用容器。

所以可以利用CSS的继承关系把div上的CSS传递给它所有子元素。

你可以用<div>来标记一个div元素的开始，然后用</div>来标记一个div元素的结束。

### html 的布局情况 padding、margin

有三个影响HTML元素布局的重要属性：padding(内边距)、margin(外边距)、border(边框)。

元素的 padding 控制元素内容 content和元素边框 border 之间的距离。

元素的外边距 margin 控制元素边框 border 和元素实际所占空间的距离。

元素的 margin 控制元素的 border 和元素实际所占空间的距离。

可以简写这写值：

除了分别指定元素的 padding-top、padding-right、padding-bottom 和 padding-left 属性外，你还可以集中起来指定它们，举例如下：

padding: 10px 20px 10px 20px;

这四个值以顺时针方式排列：顶部、右侧、底部、左侧，简称：上右下左。(注意，中间用空格隔开，而不是逗号。)
