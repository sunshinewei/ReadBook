#### Activity的启动模式和onNewIntent

##### 设置Activity的为singleTask,singleInstance,singleTop时的启动模式

此时activity在栈顶，如果直接通过跳转的话，和intent进行数据交互会出现问题，此时使用onNewIntent()进行数据处理；两个界面此时要用到Intent传值。
