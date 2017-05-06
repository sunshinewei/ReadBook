### NDK的环境搭建

1. 下载NDK，然后在path路径下配置，添加到根目录。
2. 在Android studio中在project structre->NDK中添加。
3. 采用LLDB调试程序，在SDK Manager中安装这些组件。
	1. 在打开的项目中，从菜单栏选择 Tools > Android > SDK Manager。
	2. 点击 SDK Tools 标签。
    3. 选中 LLDB、CMake 和 NDK 旁的复选框。
    4. 点击 Apply，然后在弹出式对话框中点击 OK。
	5. 安装完成后，点击 Finish，然后点击 OK。
4. 创建支持C/C++的项目。

### 创建一个支持C++/C的Demo
1. 新建工程，勾选支持C++复选框。生成的Activity不同，代码如下：
```
public class MainActivity extends AppCompatActivity {

    // Used to load the 'native-lib' library on application startup.
    static {
        System.loadLibrary("native-lib");
    }

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Example of a call to a native method
        TextView tv = (TextView) findViewById(R.id.sample_text);
        tv.setText(stringFromJNI());
    }

    /**
     * A native method that is implemented by the 'native-lib' native library,
     * which is packaged with this application.
     */
    public native String stringFromJNI();
}
```

2. 配置NDK支持，项目构建完成，出现这几个文件或文件夹。
(a). externalNativeBuild ---> cmake 编译好的文件, 显示支持的各种硬件等信息
(b). cpp ---> C 语言程序的逻辑部分, native-lib.cpp 文件名可自行修改
(c). CMakeLists.txt ---> CMake 脚本配置的文件, 具体可查阅 CMake官网的资料

3. Gradle 文件配置 CMake

```
apply plugin: 'com.android.application'

android {
    compileSdkVersion 25
    buildToolsVersion "25.0.2"
    defaultConfig {
        applicationId "com.example.administrator.cmakeexapmle"
        minSdkVersion 15
        targetSdkVersion 25
        versionCode 1
        versionName "1.0"
        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
       	//第一项
        externalNativeBuild {
            cmake {
                cppFlags ""
            }
        }
    }
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
    //第二项
    externalNativeBuild {
        cmake {
            path "CMakeLists.txt"
        }
    }
}

dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    androidTestCompile('com.android.support.test.espresso:espresso-core:2.2.2', {
        exclude group: 'com.android.support', module: 'support-annotations'
    })
    compile 'com.android.support:appcompat-v7:25.1.0'
    testCompile 'junit:junit:4.12'
}
```
只配置上面两项即可。

4. C/C++部分：

```
#include <jni.h>
#include <string>

extern "C"
jstring
Java_com_example_administrator_cmakeexapmle_MainActivity_stringFromJNI(
        JNIEnv* env,
        jobject /* this */) {
    std::string hello = "Hello from C++";
    return env->NewStringUTF(hello.c_str());
}
```

5. CMakeLists.txt 部分。

<pre><code>
# Sets the minimum version of CMake required to build the native
# library. You should either keep the default value or only pass a
# value of 3.4.0 or lower.

cmake_minimum_required(VERSION 3.4.1)

# Creates and names a library, sets it as either STATIC
# or SHARED, and provides the relative paths to its source code.
# You can define multiple libraries, and CMake builds it for you.
# Gradle automatically packages shared libraries with your APK.

add_library( # Sets the name of the library.
             native-lib

             # Sets the library as a shared library.
             SHARED

             # Provides a relative path to your source file(s).
             # Associated headers in the same location as their source
             # file are automatically included.
             src/main/cpp/native-lib.cpp )

# Searches for a specified prebuilt library and stores the path as a
# variable. Because system libraries are included in the search path by
# default, you only need to specify the name of the public NDK library
# you want to add. CMake verifies that the library exists before
# completing its build.

find_library( # Sets the name of the path variable.
              log-lib

              # Specifies the name of the NDK library that
              # you want CMake to locate.
              log )

# Specifies libraries CMake should link to your target library. You
# can link multiple libraries, such as libraries you define in the
# build script, prebuilt third-party libraries, or system libraries.

target_link_libraries( # Specifies the target library.
                       native-lib

                       # Links the target library to the log library
                       # included in the NDK.
                       ${log-lib} )

</code></pre>

`target_link_libraries`和`add_library`中`native-lib`名称可以同时更改, 注意两者需要一致, 更改名称后 会在 .externalNativeBuild 目录下生成相应的 so 的名称，Android 部分调用时 static 语块中 引入的 so 文件名也要保持一致。
