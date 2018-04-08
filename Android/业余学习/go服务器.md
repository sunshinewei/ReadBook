### 处理表单输入

Handler里面不会自动解析form,必须显式的调用下面方法。
<code>
r.ParseForm()
</code>

###  beego


#### 参数设置




#### 路由设置

routers:

<code>init()</code>函数

<pre>
func init() {
    beego.Router("/", &controllers.MainController{})
}
</pre>

#####    固定路由

即全匹配路由,一个固定的路由，一个控制器
<code>
beego.Router("/", &controllers.MainController{})
beego.Router("/admin", &admin.UserController{})
beego.Router("/admin/index", &admin.ArticleController{})
beego.Router("/admin/addpkg", &admin.AddController{})
</code>

#####    正则路由

<code>
beego.Router(“/api/?:id”, &controllers.RController{})
</code>

#####    自动路由
用户首先需要把需要路由的控制器注册到自动路由中：

<code>
beego.AutoRouter(&controllers.ObjectController{})
</code>

#### controller 逻辑


#### model 分析

我们知道 Web 应用中我们用的最多的就是数据库操作，而 model 层一般用来做这些操作，我们的 bee new 例子不存在 Model 的演示，但是 bee api 应用中存在 model 的应用。说的简单一点，如果您的应用足够简单，那么 Controller 可以处理一切的逻辑，如果您的逻辑里面存在着可以复用的东西，那么就抽取出来变成一个模块。因此 Model 就是逐步抽象的过程，一般我们会在 Model 里面处理一些数据读取，


####  View 编写



#### 静态文件处理

网页往往包含了很多的静态文件，包括图片、JS、CSS 等。

