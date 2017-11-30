

#### 动画设置
打开加载动画时：<code>homeAdapter.openLoadAnimation();</code>
<br/>设置加载动画：
<code>  mAnimationAdapter.openLoadAnimation(BaseQuickAdapter.ALPHAIN);</code>
动画形式有：
<pre><code>
    BaseQuickAdapter.ALPHAIN;//
   
   BaseQuickAdapter.SCALEIN//由放大
  
    BaseQuickAdapter.SLIDEIN_BOTTOM;//从底部滑入
   
    BaseQuickAdapter.SLIDEIN_LEFT//

	new CustomAnimation()//正常显示形式
</code></pre>


？？？？//
 mAnimationAdapter.isFirstOnly(false);//init firstOnly state

#### 混合布局
实体类必须继承MultiItemEntity
adapter继承<code>BaseMultiItemQuickAdapter</code>

构造器中
<pre><code>

 public MultipleItemQuickAdapter(Context context, List data) {
        super(data);
        addItemType(MultipleItem.TEXT, R.layout.item_text_view);//设置条目类型
        addItemType(MultipleItem.IMG, R.layout.item_image_view);
        addItemType(MultipleItem.IMG_TEXT, R.layout.item_img_text_view);
    }

</code></pre>

##### RecyclerView嵌套RecyclerView出现卡问题（添加一个ViewPool）https://www.ctolib.com/topics-116825.html
<pre><code>
RecyclerView.RecyclerViewPool pool=new RecyclerView.RecyclerViewPool();
recyclerview.setRecyclerViewPool(mSharePool);
</code></pre>

