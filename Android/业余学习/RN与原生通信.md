### React Native与原生通信

#### RN跳转到原生Activity,没有返回值。
1. 在Android studio中创建一个Activity，为TwoActivty。

2. 在React Native中调用原生的Activity时，要添加Flags在意图。
3. RN调用原生界面，用户操作原生界面后将结果返回到RN侧。
发送消息时，在APPliction中得到包管理器，在包管理器中有个module,在module中发送消息给Rn测。

4. React native进行配置，监听，通过companentWillMount(){
DeviceEventLlitter.addListener();
}