#### React Native的环境配置
1. 安装JDK和SDK并配置path变量。
```
JAVA_HOME  jdk的根目录
  ANDROID_HOME  sdk的根目录
  path中添加:%ANDROID_HOME%\platform-tools;%ANDROID_HOME%\tools```
2. 安装phyton,配置环境变量。
```
添加环境变量至path:  D:\RN\phyton;D:\RN\phyton\Scripts
```
3. 安装node.js，可以是安装版，可以是绿色版（配置环境变量）。
4. 安装React Native,通过下面命令：
```
npm install -g react-native-cli ```
5. 切换到你的工作空间，创建工程，如Demo,通过命令
```
react-native init Demo 
```
如果创建工程太慢，在nodejs中的文件找到nodejs\node_modules\npm找到文件npmrc，打开后在该文件末尾一行加上
```
registry = https://registry.npm.taobao.org
```
6. 文件创建成功后，进行测试是否创建成功，进入到Demo文件夹下，输入如下命令：
```
react-native start
```
在浏览器中输入如下，看是否创建成功：
```
http://localhost:8081/index.android.bundle?platform=android
```
7. 在android设备上运行命令：
```
react-native run-android
```
8. 在ios设备上运行命令：
```
react-native run-ios
```