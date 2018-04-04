### 注解
应用于类、方法、参数、变量、构造器及包声明中的特殊修饰符。

假如你想为应用设置很多的常量或参数，这种情况下，XML是一个很好的选择，因为它不会同特定的代码相连。如果你想把某个方法声明为服务，那么使用Annotation会更好一些，因为这种情况下需要注解和方法紧密耦合起来，开发人员也必须认识到这点。


Annotations仅仅是元数据，和业务逻辑无关


##### 注解元素取值（通过反射机制拿的值）
<pre>
<code>
@Target(ElementType.FIELD)
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface TagetValue {

    TagetParam value() default TagetParam.TYPETWO;//枚举类型

    String valueName() default "a";

    int valueAge() default 8;
}
</code>
<code>
调用取值
@TagetValue(valueAge = 9)
    private int age;

    @TagetValue(valueName = "xiaoli")
    private String name;

    @TagetValue(TagetParam.TYPEFOUR)
    private TagetParam tagetParam;
    
    Field[] declaredFields = MainActivity.class.getDeclaredFields();

        for (int i = 0; i < declaredFields.length; i++) {

            if (declaredFields[i].isAnnotationPresent(TagetValue.class)){

                TagetValue annotation = declaredFields[i].getAnnotation(TagetValue.class);

                System.out.println("长度2"+annotation.toString()+i);

                param=annotation.valueName()+"    "+annotation.valueAge()+"   "+annotation.value().toString();
            }
        }
</code>
<code>
也可以同时这样注解,此时取值不循环，真确
 @TagetValue(value = TagetParam.TYPEFOUR,valueName ="xscc",valueAge =18)
</code>
</pre>

类上面的注解
<pre>
<code>
取注解上的值
  TagetValue annotation = MainActivity.class.getAnnotation(TagetValue.class);
   tv.setText(annotation.valueAge()+"   "+annotation.valueName());
</code>
</pre>

