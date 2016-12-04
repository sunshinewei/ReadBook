#Activity
###Activity的生命周期
<code>onCreate()---->onStart()---->onPause()----->onResume()---->onPause()----->onStop()---->onDestory()</code>
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
<pre><code>
- Intent.FLAG_ACTIVITY_NEW_TASK:
使用一个新的Task启动一个Activity.
- FLAG_ACTIVITY_SIGNLE_TOP:
跟SignleTop启动模式一样。
- FLAG_ACTIVITY_CLEAR_TOP:
使用SignleTask启动一个Activity
- FLAG_ACTIVITY_NO_HISTORY:
~使用该模式启动一个Activity后，该Activity就会消失，不会在任务栈中~
- FLAG_ACTIVITY_EXCLUDE_FROM_RECENTS:
该标记的Acyivity不会出现在历史Activity的列表中，有时候我们不希望我们的Activity返回到历史的列表中，我们就采用次标记。</code></pre>
###IntentFilter的匹配规则
~一个Activity可以有多个intent-filter.~
#####action的匹配规则：
~Intent中的action必须能够和过滤规则中的action匹配，就是说和action的字符串完全一致。在一个过滤规则中有多个action，只要匹配一个intent中的action能够和过滤规则中的任何一个action相同即可匹配。同时需要注意的是，action是区分大小写的。~
#####category的匹配规则：
~与actionn不同，如果intent中出现category，不管有几个category，他都必须与intent匹配。~
#####data的匹配规则：
~data的过滤规则与action的相似，但是data的结构不同于action和category。~
data的结构，有两部分组成，mimeType和URI两部分组成，mimeType是指媒体类型，例：image/jpeg等，URI的结构如下：
<code><scheme>://<host>:<port>/[<path>|<pathPrefix>|<pathPattern>]</code>
scheme:URI的模式，比如http、file、content等如果URI中没有指定scheme，则整个URI无效。
Host:URI的主机名，
port:URI的端口号。
path、pathPrefix、pathPattern:表示路径消息，path表示完整的路径，pathPattern:表示完整的路径消息，可以含有通配符；pathPrefix:路径的前缀消息。
URI默认值为file/content.
**注意，如果intent中指定了完整的data,就必须调用<code>setDataAndType</code>方法，而不能调用<code>setData</code>或<code>setType</code>,这两个方法会相互清除对方的值。**