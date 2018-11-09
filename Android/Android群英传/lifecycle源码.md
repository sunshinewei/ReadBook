lifecycle,LiveData,ViewModel的源码分析

####  Lifecycle如何检测生命周期
Lifecycle是一个抽象类，它里面定义了三个抽象方法，两个枚举类型，其中三个抽象方法通过注解的形式表示在主线程中，Lifecycle的源码：
<pre><code>
public abstract class Lifecycle {
    public Lifecycle() {
    }

    @MainThread
    public abstract void addObserver(@NonNull LifecycleObserver var1);

    @MainThread
    public abstract void removeObserver(@NonNull LifecycleObserver var1);

    @MainThread
    @NonNull
    public abstract Lifecycle.State getCurrentState();

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
}
</code></pre>

前两个方法分别是添加和解除绑定，就不多说了，后边的两个枚举的作用是为实现LifecycleObserver接口里面的方法添加注解提供，让实现此接口的方法在某个生命周期时执行。如：
<pre><code>
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
</code></pre>

而LifecycleObserver接口里面本身没有任何操作，源码：
<pre><code>
public interface LifecycleObserver {

}
</code></pre>

最后将整个流程联系起来，通过Activity里的getLifecycle方法，将Activity的生命周期获取到，然后通过lifecycle里的addObserver订阅。

最后实现LifecycleHelper接口的方法结果如下：


