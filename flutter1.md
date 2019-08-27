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


在flutter中点击退出按钮不直接退出应用程序，隐藏到后台的解决方法：
<pre><code>
import android.os.Bundle;
import android.os.Looper;

import io.flutter.app.FlutterActivity;
import io.flutter.plugins.GeneratedPluginRegistrant;

import android.view.KeyEvent;
import android.content.Intent;
import android.widget.Toast;

import io.flutter.plugin.common.MethodChannel;


public class MainActivity extends FlutterActivity {
    //通讯名称,回到手机桌面
    private final String chanel = "android/back/desktop";
    //返回手机桌面事件
    static final String eventBackDesktop = "backDesktop";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        GeneratedPluginRegistrant.registerWith(this);
        initBackTop();
    }
    

    //注册返回到手机桌面事件
    private void initBackTop() {
        new MethodChannel(getFlutterView(), chanel).setMethodCallHandler(
                (methodCall, result) -> {
                    if (methodCall.method.equals(eventBackDesktop)) {
                        moveTaskToBack(false);
                        result.success(true);
                    }
                }
        );
    }
}
</code></pre>
在flutter中定义
<pre><code>
import 'package:flutter/services.dart';
import 'package:flutter/material.dart';

class AndroidBackTop {
  ///通讯名称,回到手机桌面
  static const String chanel = "android/back/desktop";

  //返回手机桌面事件
  static const String eventBackDesktop = "backDesktop";

  ///设置回退到手机桌面
  static Future<bool> backDesktop() async {
    final platform = MethodChannel(chanel);
    try {
      await platform.invokeMethod(eventBackDesktop);
    } on PlatformException catch (e) {
      debugPrint(e.toString());
    }
    return Future.value(false);
  }
}
  </code></pre>
  
  在要退出的页面写：
<pre><code>
@override
  Widget build(BuildContext context) {
 
    return WillPopScope(
      onWillPop: AndroidBackTop.backDesktop, //页面将要消失时，调用原生的返回桌面方法
      child: new Scaffold(
        body: pageData[currentPosition],
        bottomNavigationBar: botNavBar,
      ),
    );
  }
  </code></pre>
  
  flutter打包时，报如下错误：
  java.lang.UnsatisfiedLinkError: dalvik.system.PathClassLoader[DexPathList[[zip file 
    "/data/app/包名-ByONc3XVTut87IekSqMjdg==/base.apk"],nativeLibraryDirectories=
    [/data/app/包名-ByONc3XVTut87IekSqMjdg==/lib/arm64, /data/app包名-
    ByONc3XVTut87IekSqMjdg==/base.apk!/lib/arm64-v8a, /system/lib64, /vendor/lib64]]] couldn't find 
    "libflutter.so"
    
    可以做如下修改：
    <pre><code>
    defaultConfig {
      ......
        ndk {
            abiFilters "armeabi-v7a", "x86"
        }
    }
    </code></pre>
    
    
    
  检测flutter返回键监听
  <code>
WillPopScope(
        child: Scaffold(),onWillPop: (){});
</code>

如何使用flutter隐藏软键盘
<code>
  FocusScope.of(context).requestFocus(FocusNode())
  <code>
  
