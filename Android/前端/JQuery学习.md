### JQury的学习

#### JQury的function学习

html页面：
```
<div class="container-fluid">
  <h3 class="text-primary text-center">jQuery Playground</h3>
  <div class="row">
    <div class="col-xs-6">
      <h4>#left-well</h4>
      <div class="well" id="left-well">
        <button class="btn btn-default target" id="target1">#target1</button>
        <button class="btn btn-default target" id="target2">#target2</button>
        <button class="btn btn-default target" id="target3">#target3</button>
      </div>
    </div>
    <div class="col-xs-6">
      <h4>#right-well</h4>
      <div class="well" id="right-well">
        <button class="btn btn-default target" id="target4">#target4</button>
        <button class="btn btn-default target" id="target5">#target5</button>
        <button class="btn btn-default target" id="target6">#target6</button>
      </div>
    </div>
  </div>
</div>
```

```
<script>
$(document).ready(function(){

});
</script>
```

jQuery通过选择器来选择一个元素的，然后操作元素做些改变。

给标签，well类选择器和target3的id选择器添加一个动画：为`animated shake`
```
$(document).ready(function(){
    $("button").addClass("animated bounce");
    $(".well").addClass("animated shake");
    $("#target3").addClass("animated fadeOut");
     $("button").removeClass("btn-default");//移除一个选择器
      $("#target1").css("color","red");//给字体添加颜色
 });
 
 $("#target1").prop("disabled",true);//按钮变成不可选
```

你还可以用jQuery改变除了CSS以外的属性。比如，你可以让按钮变不可选。

当你把按钮设置成不可选以后，这会让按钮变灰并且不能点击。

jQuery有一个.prop()的方法让你来调整元素的属性.

jQuery不仅可以改变元素开始标记和结束标记间的文本，甚至可以改变元素标记本身。

jQuery的.html()方法可以添加HTML标签和文字到元素，而元素之前的内容都会被方法的内容所替换掉。

我们是通过em[emphasize]标签来重写和强调标题文本的：

$("h3").html("<em>jQuery Playground</em>");

jQuery 还有一个类似的方法叫.text()，它只能改变文本但不能修改标记。换句话说，这个方法只会把传进来的任何东西(包括标记)当成文本来显示。

jQuery 有一个.remove() 的方法可以移除HTML元素

jQuery有一个appendTo()方法可以把选中的元素加到其他元素中。

比如，你想让target4从我们的从right-well移到left-well，我们可以这样使用:
```
$("#target4").appendTo("#left-well");
```

除了移动元素，你还可以拷贝元素。简单理解：移动元素就是剪切，拷贝元素就是复制。

jQuery的clone()方法可以拷贝元素。

比如，如果我想把target2从left-well拷贝到right-well，我们可以这样写:

`$("#target2").clone().appendTo("#right-well");`

每个HTML元素根据继承属性都有父parent元素。

举个例子，h3 元素的父元素是 <div class="container-fluid">，<div class="container-fluid">的父元素是 body。

jQuery有一个方法叫parent()，它允许你访问指定元素的父元素。

举个例子：让left-well 元素的父元素parent()的背景色变成蓝色。

`$("#left-well").parent().css("background-color", "blue")
`

许多HTML元素都有children(子元素)，每个子元素都从父元素那里继承了一些属性。

举个例子，每个HTML元素都是 body 的子元素， 你的 "jQuery Playground" h3 元素是 <div class="container-fluid"> 的子元素。

jQuery有一个方法叫children()，它允许你访问指定元素的子元素。

举个例子：让left-well 元素的子元素children()的文本颜色变成蓝色。

`$("#left-well").children().css("color", "blue");`

jQuery有一些另外的技巧可以达到同样的效果。

jQuery 用CSS选择器来选取元素，target:nth-child(n) CSS选择器允许你按照索引顺序(从1开始)选择目标元素的所有子元素。

示例：你可以给目标元素的第三个子元素添加bounce class。

`$(".target:nth-child(3)").addClass("animated bounce");`

获取class为target且索引为奇数的所有元素，并给他们添加class。

$(".target:odd").addClass("animated shake");

记住，jQuery里的索引是从0开始的，也就是说：:odd 选择第2、4、6个元素，因为target#2(索引为1)，target#4(索引为3)，target6(索引为5。
奇数：odd,偶数：even。