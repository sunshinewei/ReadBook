### Android原生与JS交互：

#### WebView加载本地Html文件时:
<code>webView.loadUrl("file:///android_asset/XX.html")</code>


#### html的例子<code>javascript:button.click0()</code>中的button是原生webView.addJavascriptInterface(param1,param2)中的第二个参数

<pre>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
        "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
    <title>这里是一个H5页面</title>
</head>

<body><code>
<p id="ptext">点击按键0 执行android中的 public void click0(){} 方法</p>
<Button id="buttonId0" class="buttonClass" onclick="javascript:button.click0()">按键0</Button>
<p>点击按键1 执行android中的 public void click0(String data1,String data2){}方法</p>
<Button id="buttonId1" class="buttonClass" onclick="javascript:button.click0('参数1','参数2')">按键1
</Button>

<script>
        function setRed(){
        //这个方法设置 id 为 ptext 的元素的背景色为红色
        var a = document.getElementById('ptext');
        a.style.backgroundColor="#F00";
    }
    function setColor(color,text){
        //这个方法设置 id 为 ptext 的元素的背景色为指定颜色
        //设置 id 为 ptext 的元素的内容为text
        var a = document.getElementById('ptext');
        a.style.backgroundColor=color;
        a.innerHTML = text;
    }

</script>
</body>
</code></pre>


#### 原生Android中设置Webview
<pre>
 settings.setJavaScriptEnabled(true);  //设置运行使用JS
        ButtonClick click = new ButtonClick();
        //这里添加JS的交互事件，这样H5就可以调用原生的代码
        webView.addJavascriptInterface(click,click.toString());
</pre>

#### JS向Android中发送消息(在原生方法前加注解<code> @JavascriptInterface</code>)
<pre>
  class ButtonClick{

        //这是 button.click0() 的触发事件
        //H5调用方法：javascript:button.click0()
        @JavascriptInterface
        public void click0(){
            show("title","");
        }

        //这是 button.click0() 的触发事件，可以传递待参数
        //H5调用方法：javascript:button.click0('参数1','参数2')
        @JavascriptInterface
        public void click0(String data1,String data2){
            show(data1,data2);
        }


        @Override
        @JavascriptInterface  //必须添加，这样才可以标志这个类的名称是 button
        public String toString(){
            return "button";
        }

        private void show(String title,String data){
//            new AlertDialog.Builder(getWindow().getContext())
//                    .setTitle(title)
//                    .setMessage(data)
//                    .setPositiveButton("确定",null)
//                    .create().show();
            startActivity(new Intent(MainActivity.this,TwoActivity.class));
        }
    }
}
</pre>

#### Android 原生向JS发送消息(<code>setRed()</code>JS中定义的方法名)

<pre>
webView.loadUrl("javascript:setRed()");
</pre>

#### 请求同步Cookie
<pre>
 
public static void synCookies(Context context, String url) {  
    CookieSyncManager.createInstance(context);  
    CookieManager cookieManager = CookieManager.getInstance();  
    cookieManager.setAcceptCookie(true);  
    cookieManager.removeSessionCookie();//移除  
    cookieManager.setCookie(url, cookies);//cookies是在HttpClient中获得的cookie  
    CookieSyncManager.getInstance().sync();  
}
</pre>

在html换起app：
<intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            
            
            
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:host="splash" android:scheme="cundong" />
       </intent-filter>
      地址是：
     src="cundong://splash"


