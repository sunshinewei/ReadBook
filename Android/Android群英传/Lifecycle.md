Lifecycle:官方介绍
Lifecycle is a class that holds the information about the lifecycle state of a component (like an activity or a fragment) and allows other objects to observe this state.
Lifecycle uses two main enumerations to track the lifecycle status for its associated component。
大概意思是：
生命周期它保存关于组件的生命周期状态（如Activity和Fragment）的信息，并允许其他对象观察此状态。
生命周期使用枚举来跟踪其相关组件的生命周期状态。看源码：（一个记录State，一个记录Event）。
```
 public static enum State {
        DESTROYED,
        INITIALIZED,
        CREATED,
        STARTED,
        RESUMED;
        private State() {
        }
        public boolean isAtLeast(@NonNull Lifecycle.State state) {
            return this.compareTo(state) >= 0;
        }
    }
    public static enum Event {
        ON_CREATE,
        ON_START,
        ON_RESUME,
        ON_PAUSE,
        ON_STOP,
        ON_DESTROY,
        ON_ANY;
        private Event() {
        }
    }
```
通过一个例子学会控制Activity的生命周期，在各生命周期完成事件：
首先定义一个接口，让其继承LifecycleObserver，在Activity实现此接口：

```
public interface LifecycleHelper extends LifecycleObserver {
    @OnLifecycleEvent(Lifecycle.Event.ON_START)
    void onStartLifecycle();
    @OnLifecycleEvent(Lifecycle.Event.ON_CREATE)
    void onCreateLifecycle();
    @OnLifecycleEvent(Lifecycle.Event.ON_RESUME)
    void onResumeLifecycle();
    @OnLifecycleEvent(Lifecycle.Event.ON_PAUSE)
    void onPauseLifecycle();
    @OnLifecycleEvent(Lifecycle.Event.ON_STOP)
    void onStopLifecycle();
    @OnLifecycleEvent(Lifecycle.Event.ON_DESTROY)
    void onDestoryLifecycle();
}
```
在onCreate()中订阅：

```
 getLifecycle().addObserver(this);
```
在onDestory()解订阅：

```
 getLifecycle().removeObserver(this);
```
如下：

```
public class TeastActivity extends AppCompatActivity implements LifecycleHelper {

    @Override
    protected void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_teast);
        getLifecycle().addObserver(this)；
    }
    @Override
    protected void onDestroy() {
        super.onDestroy();
        getLifecycle().removeObserver(this);
    }

    @Override
    public void onStartLifecycle() {
    }
    
    @Override
    public void onCreateLifecycle() {
    }

    @Override
    public void onResumeLifecycle() {
    }

    @Override
    public void onPauseLifecycle() {
    }

    @Override
    public void onStopLifecycle() {
    }

    @Override
    public void onDestoryLifecycle() {
    }
}
```
