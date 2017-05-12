### 响应式框架Bootstrap
Bootstrap将会根据你的屏幕的大小来调整HTML元素的大小 —— 强调 响应式设计的概念。

通过响应式设计，你无需再为你的网站设计一个手机版的。它在任何尺寸的屏幕上看起来都会不错。

你仅需要通过添加下列代码到你的HTML开头来将Bootstrap添加到任意应用中：
<pre>
    <link rel="stylesheet" href="//cdn.bootcss.com/bootstrap/3.3.1/css/bootstrap.min.css"/>
</pre>

使用Bootstrap时：我们需要把所有的HTML内容放在class为container-fluid的div下。

#### 对于图片的设置：
  通过Bootstrap，我们要做的只是给图片添加 img-responsive class属性。这样图片的宽度就能完美地适配你的页面的宽度了。
  如：
<pre>
   <img src="/images/running-cat.jpg" class="img-responsive"/>
</pre>

#### 网格布局
Bootstrap 使用一种响应式网格布局——可轻松实现将多个元素放入一行并指定各个元素的相对宽度的需求。Bootstrap 中大多数的class属性都可以设置于 div 元素中。

如：
<pre>
<div class="col-xs-4">
    <div class="row">
    <button class="btn btn-block btn-primary">Like</button>
    </div>
  </div>
  <div class="col-xs-4">
    <div class="row">
    <button class="btn btn-block btn-info">Info</button>
    </div>
  </div>
  <div class="col-xs-4">
    <div class="row">
    <button class="btn btn-block btn-danger">Delete</button>
    </div>
  </div>
</pre>
将会使用 col-xs-* ，其中 xs 是 extra small 缩写（应用于较小的屏幕，比如手机屏幕），* 是你需要填写的数字（之和总共12），代表在一行中,各个元素应该占的列宽。

把 Like, Info 和 Delete 三个按钮一并放入一个 <div class="row"> 元素中；然后，其中的每一个按钮都需要各自被一个 <div class="col-xs-4"> 元素包裹。

当div 元素设置了 class 属性 row 之后，那几个按钮便可嵌入其中。

#### span标签
可以用 span 标签来创建行内元素
通过使用 span 元素，你可以把几个元素放在一起。你甚至可以用此为一个元素的不同部分指定样式。

Bootstrap使用响应式栅格系统，这使得把元素放入行内并为每个元素指定宽度变得很容易。大部分的 Bootstrap的 class 都可以被用在 div 元素上。
如：
<pre>
<div class="row">
  <div class="col-xs-8">
     <h2 class="text-primary text-center">CatPhotoApp</h2>
  </div>
  <div class="col-xs-4"
     <a href="#"><img class="img-responsive thick-green-border" src="/images/relaxing-cat.jpg"></a>
  </div>
</div>
</pre>

#### Bootsstrap与radio button结合使用
 Bootstrap 的 col-xs-*用在 form 元素中。这样的话，我们的单选按钮就可以均匀地在页面上展开，不需要知道屏幕的分辨率有多宽。

#### well标签
Bootstrap 有一个 class 属性叫做 well，它的作用是为设定的列创造出一种视觉上的深度感（一种视觉上的效果，动手写代码体会一下）。

在你的每一个class为col-xs-6的div 元素中都嵌入一个带有 well class 属性的 div 元素。
