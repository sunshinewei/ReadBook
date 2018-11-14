在官方文档中是这样说的：
LiveData是一个可观察的数据持有者类。与常规observable不同的是LiveData可以关联Activity,Fragment,Services的生命周期。保证了当在组件的生命周期的发生变化是LiveData会发生更新。
使用LiveData的优点有：
1.确保了数据源与UI的一致： LiveData遵循观察者模式。Observer生命周期状态更改时，LiveData会通知 对象。您可以合并代码以更新这些Observer对象中的UI 。每次应用程序数据更改时，观察者都可以在每次更改时更新UI，而不是更新UI。
2.没有内存泄漏：绑定在Lifecycle对象上，生命周期结束，自动解除。
3.当Activity停止时，不会造成crash(官方文档的解释如下)
If the observer's lifecycle is inactive, such as in the case of an activity in the back stack, then it doesn’t receive any LiveData events.
由于LiveData存在onActive和onInactive两种状态，当调用onActive表示有观察者，会接收Event的改变。
4.不需要我们去处理生命周期：由于是一个观察者，当UI组件的生命周期发生变化是，LiveData会自动的处理，不需要更多的考虑。
5.保持着最新的数据：如果生命周期变为非活动状态，则会在再次变为活动状态时接收最新数据。例如，后台活动在返回前台后立即收到最新数据。
6.适配设备配置变化：比如如屏幕旋转，立即收到上次的数据。
7.资源共享：是对LiveData的扩展，使用单例模式。
通过源码看LiveData有以上有点：
```
@MainThread
    public void observe(@NonNull LifecycleOwner owner, @NonNull Observer<T> observer) {
        if(owner.getLifecycle().getCurrentState() != State.DESTROYED) {
            LiveData<T>.LifecycleBoundObserver wrapper = new LiveData.LifecycleBoundObserver(owner, observer);
            LiveData<T>.ObserverWrapper existing = (LiveData.ObserverWrapper)this.mObservers.putIfAbsent(observer, wrapper);
            if(existing != null && !existing.isAttachedTo(owner)) {
                throw new IllegalArgumentException("Cannot add the same observer with different lifecycles");
            } else if(existing == null) {
                owner.getLifecycle().addObserver(wrapper);
            }
        }
    }
```
可以看到，当调用observe方法是，Activity或者Fragment本身实现了LifecycleOwner接口，通过`Lifecycle getLifecycle();`拿到他们的Lifecycle，最后一句代码`owner.getLifecycle().addObserver(wrapper);`此时我们知道他内部调用和lifecycle的使用一样，通过订阅的方式，当组件生命周期结束后，解除订阅。在这里有一重要的是，在他调用观察者时。判断了生命周期是否结束。`owner.getLifecycle().getCurrentState() != State.DESTROYED`这样保证了当Activity销毁掉，不会导致Crash。
在内部有一个观察者专门检测组件的生命周期：
```
public void onStateChanged(LifecycleOwner source, Event event) {
          //当组件销毁了，直接移除观察者，否则调整LiveData的状态。
            if(this.mOwner.getLifecycle().getCurrentState() == State.DESTROYED) {
                LiveData.this.removeObserver(this.mObserver);
            } else {
                this.activeStateChanged(this.shouldBeActive());
            }
        }
```
移除观察者：

```
 @MainThread
    public void removeObserver(@NonNull Observer<T> observer) {
    //判断当前线程，没有在主线程直接抛出异常
        assertMainThread("removeObserver");
        LiveData<T>.ObserverWrapper removed = (LiveData.ObserverWrapper)this.mObservers.remove(observer);
        if(removed != null) {
            removed.detachObserver();
            removed.activeStateChanged(false);
        }
    }
    @MainThread
    public void removeObservers(@NonNull LifecycleOwner owner) {
        assertMainThread("removeObservers");
        Iterator var2 = this.mObservers.iterator();
        while(var2.hasNext()) {
            Entry<Observer<T>, LiveData<T>.ObserverWrapper> entry = (Entry)var2.next();
            if(((LiveData.ObserverWrapper)entry.getValue()).isAttachedTo(owner)) {
                this.removeObserver((Observer)entry.getKey());
            }
        }
    }
```
LiveData设置值：通过源码可以看到，有postValue和setValue两种，而postValue实在其他线程中设置，setValue在主线程中调用。
```
protected void postValue(T value) {
        Object var3 = this.mDataLock;
        boolean postTask;
        synchronized(this.mDataLock) {
            postTask = this.mPendingData == NOT_SET;
            this.mPendingData = value;
        }
        if(postTask) {
            ArchTaskExecutor.getInstance().postToMainThread(this.mPostValueRunnable);
        }
    }

    @MainThread
    protected void setValue(T value) {
        assertMainThread("setValue");
        ++this.mVersion;
        this.mData = value;
        this.dispatchingValue((LiveData.ObserverWrapper)null);
    }
```
