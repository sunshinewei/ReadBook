#android性能优化
####1.布局优化
1.android系统提供了检测UI的渲染时间的工具，在开发者模式中，GPU的绘制渲染时所需要的时间；
2.避免重绘：android系统中过度重绘，给了三种颜色，对于开发者来说，尽量增加蓝色区域，减少红色区域；
3.优化布局层级，对于android中每个view都是一个树状图，如果树的高度太高，这样会严重影像测量、布局和绘制的速度，所以要降低View树的高度。
4.避免嵌套过多的无用布局；
5.使用<include>标签重用layout:在开发中遇到一些共性的UI，对于这些将其单独提出，然后用include标签应用。
6.使用<ViewStub>实现View的延迟加载；是一个轻量级的组件，他不仅不可视，大小为0；对于ViewStub标签应用的布局，可以使用VISIBLE和inflate（）使其显示，对于inflate()来说，返回一个应用布局，可以通过这个应用布局的findViewById来找到对应的控件.
View inflate = mViewStub.inflate();对于ViewStub调用两次inflate()会报错，由于ViewStub被设置为可见，或被inflate了，ViewStub就不存在了。在整个布局初始化时，view添加到了布局树中，而viewstub没有，在渲染后才添加到布局树种。
7.H Viewer的使用：三个按钮，绿、黄、红代表了好、中、差。
####2.内存优化