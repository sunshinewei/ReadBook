#### Flutter的环境搭建



flutter中ListView嵌套GrideView解决办法：
出现这种情况可在GridView中设置shrinkWrap:true即可解决：
GridView.count(
  shrinkWrap:true,                              // 处理listview嵌套报错
),
在GrideView外边包一层布局：
Container(
                        width: CommonUtil.getScreenWidth(context) - 60.0,
                        child: new ImageGrideView(item.attributE1), )

此时有可能出现手指在GridView区域滑动时ListView无法进行滚动，处理该问题可在GridView中设置physics: NeverScrollableScrollPhysics()来处理：
GridView.count(
  physics: NeverScrollableScrollPhysics(),      // 处理GridView中滑动父级Listview无法滑动
)
　　
  
  
  
  
  
SingleChildScrollView嵌套ListView或者GrideView使用，解决滑动冲突事件，SingleChildScrollView让永远滑动，ListView采用physics: const NeverScrollableScrollPhysics(),shrinkWrap: true,即可解决。
