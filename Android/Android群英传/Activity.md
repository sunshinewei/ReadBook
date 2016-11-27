#Activity
###Activity的生命周期
~onCreate()---->onStart()---->onPause()----->onResume()---->onPause()----->onStop()---->onDestory();~
######Paused状态
~表示当Activity失去其焦点，被一个新的非全屏的Activity或者一个透明的Activity放在栈顶时，转换为Paused状态，他失去与用户交互的能力，所有的信息成员变量还保持着。但在系统内存极低的情况下，会被系统回收掉。~
#####Activity重新创建的过程
~如果系统长期处于stop形态，且系统需要更多内存或内存紧张时，系统会回收Activity,此时会将Activity状态通过onSaveInstanceState()方法保存到Bundle对象中，当你重新创建这个Activity时，保存到Bundle对象就会传递到Activity的onRestoreInstanceState()方法与onCreate()方法中。~
####Android任务栈
~在Android中，通过栈结构保存整个App的Activity,栈低的元素是整个任务1的发起者，当一个App启动后，如果当前App不存在App的任务栈，系统就会创建一个，这个App启动的所有Activity都将在这个任务栈中被管理。这个栈被称为Task,同时，一个Task中的Activity可以来自不同的App,同一个App的Activity也可能不在同一个Task中。~
####Activity的启动模式
1.Standard:
~这种模式启动一个Activity时，每次实例化。~
2.SignleTop:
~这种启动模式启动一个Activity,系统检测当前栈顶的Activity是否是要启动的Activity,如果是，不实例。这种启动模式在聊天界面，每次接收消息后显示的界面；微信的支付界面。~
3.SignleTask:
~如果以这种方式启动一个Activity,他将创建一个新的任务栈。~
4.SignInstance:
~会创建一个新的任务栈，且该任务栈中只存在这一个Activity。如果应用A创建一个MainActivity,且启动模式为此模式，如果B应用也要激活MainActivity,则不需要创建，两者应该共享。~
**SignleTask和SignleInstance中使用startActivityForResult()方法来启动另一个ActivityB,这种情况系统直接返回Activity.RESULT_CANCELED,而不再去等待返回。这种情况只能通过Intent来绑定数据。**
#####Intent Flag启动模式
- Intent.FLAG_ACTIVITY_NEW_TASK:
~使用一个新的Task启动一个Activity.~
- FLAG_ACTIVITY_SIGNLE_TOP:
~跟SignleTop启动模式一样。~
- FLAG_ACTIVITY_CLEAR_TOP:
~使用SignleTask启动一个Activity~
- FLAG_ACTIVITY_NO_HISTORY:
~使用该模式启动一个Activity后，该Activity就会消失，不会在任务栈中~
