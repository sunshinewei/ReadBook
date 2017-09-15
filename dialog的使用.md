### 常用网址收藏

#### 关于弹出框Dialog

<pre>
关于加载中，或删除成功等dialog:
https://github.com/pedant/sweet-alert-dialog

关于任意位置的dialog
https://github.com/orhanobut/dialogplus


https://github.com/H07000223/FlycoDialog_Master

底部对话框
https://github.com/shaohui10086/BottomDialog
</pre>

#### 关于FlycoDialog_Master的使用：
##### 底部条目
<pre><code>
String[] stringItems = {"接收消息并提醒", "接收消息但不提醒", "收进群助手且不提醒", "屏蔽群消息"};
        final ActionSheetDialog dialog = new ActionSheetDialog(mContext, stringItems, null);
        dialog.title("选择群消息提醒方式\r\n(该群在电脑的设置:接收消息并提醒)")//
                .titleTextSize_SP(14.5f)//
                .show();

        dialog.setOnOperItemClickL(new OnOperItemClickL() {
            @Override
            public void onOperItemClick(AdapterView<?> parent, View view, int position, long id) {
                toastLong(stringItems[position]);
                dialog.dismiss();
            }
        });
</code></pre>

#### 对PopupWindow的使用

<pre><code>
 new BubblePopup(mContext, inflate)
                .anchorView(mBut)
                .bubbleColor(mContext.getResources().getColor(R.color.white))
                .gravity(Gravity.BOTTOM)
                .showAnim(null)
                .dismissAnim(null)
                .show();
</code></pre>

#### 自定义Dialog的基本设置：

##### 在样式中的基本配置

<style name="dialog" parent="@android:style/Theme.Dialog">
    //Dialog的windowFrame框为无
    <item name="android:windowFrame">@null</item>
    //是否浮现在activity之上
    <item name="android:windowIsFloating">true</item>
    //是否半透明
    <item name="android:windowIsTranslucent">true</item>
    //是否显示title
    <item name="android:windowNoTitle">true</item>
    //设置dialog的背景
    <item name="android:background">@android:color/transparent</item>
    //显示区域背景是否透明
    <item name="android:windowBackground">@android:color/transparent</item>
    //就是用来控制灰度的值，当为1时，界面除了我们的dialog内容是高亮显示的，dialog以外的区域是黑色的，完全看不到其他内容，系统的默认值是0.5
    <item name="android:backgroundDimAmount">0.5</item>
    //显示区域以外是否使用黑色半透明背景
    <item name="android:backgroundDimEnabled">true</item>
</style>

#### 自定义Dialg在构造器中应用，如
<pre><code>

    public BaseDilog(@NonNull Context context) {
        super(context,R.style.MyDialog);//应用style中的东西
    }

    public BaseDilog(@NonNull Context context, @StyleRes int themeResId) {
        super(context, themeResId);
    }

    protected BaseDilog(@NonNull Context context, boolean cancelable, @Nullable OnCancelListener cancelListener) {
        super(context, cancelable, cancelListener);
    }
</code></pre>

##### Dailog从底部弹出，并点击其他区域不消失
<pre><code>
  Window window = baseDilog.getWindow();
                WindowManager.LayoutParams attributes = window.getAttributes();
                attributes.width=WindowManager.LayoutParams.MATCH_PARENT;
                attributes.height=WindowManager.LayoutParams.WRAP_CONTENT;

                attributes.gravity=Gravity.BOTTOM;
                window.setAttributes(attributes);
                baseDilog.setCancelable(false);
</pre></code>