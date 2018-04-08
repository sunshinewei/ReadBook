### Observer(观察者）

<pre>
onSubscribe();
onNext();
onError()；
onComplete()；
</pre>


### Observable（被观察者）


#### Function函数（输入一个类型的值，可以返回其他类型的值）

实现类型的转换

**
/**
 * A functional interface that takes a value and returns another value, possibly with a
 * different type and allows throwing a checked exception.
 *
 * @param <T> the input value type
 * @param <R> the output value type
 */
public interface Function<T, R> {
    /**
     * Apply some calculation to the input value and return some other value.
     * @param t the input value
     * @return the output value
     * @throws Exception on error
     */
    R apply(@NonNull T t) throws Exception;
}
**






