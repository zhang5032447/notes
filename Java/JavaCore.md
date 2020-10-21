

### 1. 数组

### 2. 链表

特点

> 1. 灵活的空间要求，存储空间不要求连续
> 2. 不支持下标的访问，支持顺序遍历检索
> 3. 针对<span style='color:red'>增删</span>效率更高

### 3. 树

##### 红黑树

> 1. 每个节点要么是红色，要么是黑色
> 2. 每个跟节点是黑色
> 3. 每个叶子节点是黑色
> 4. 每个红色节点的两个子节点必须是黑色
> 5. 任意节点到每个叶子节点的路径包含相同数量的黑节点`黑色节点平衡`

> 1. Recolor 重新标注节点颜色
> 2. rotaion 通过旋转达到平衡

红黑树能自平衡，三种操作：左旋，右旋，变色

> 左旋：以某个节点作为支点，其右子节点变为旋转的父节点，右子节点的左子节点变为旋转节点的右子节点，左子节点保持不变。
>
> 右旋：以某个节点作为支点，其左子节点变为旋转的父节点，左子节点的右子节点变为旋转节点的左子节点，右子节点保持不变。
>
> 变色：节点的颜色由红变黑或由黑变红。

### 4. 集合

#### ArrayList

#### LinkedList

#### Vector

#### Collections.synchronizedList

#### HashSet

#### TreeSet

### Map接口

> Map集合的特点
>
> 1. 能够存储唯一的列表的数据（唯一，不可重复）Set
> 2. 能够存储可以重复的数据（可重复）List
> 3. 值得顺序取决于键的顺序
> 4. 键和值都是可以存储null元素

#### TreeMap

本质上就是红黑树的实现

> 1. 

#### HashMap



## 泛型

本质：参数化类型

#### 泛型的擦除：

​	泛型只在编译阶段有效，编译之后JVM会采取去泛型化的措施。

​	泛型在运行阶段没有效果

#### 通配符

1. 无边界通配符

> <?>

2. 上边界通配符

> <? extends Number>  代表继承Number的子类的对象都可以

3. 下边界通配符

> <? super Integer> 代表从Integer到Object所有的对象都可以 

### 泛型的具体使用

规则

> 必须先声明在使用

> 泛型的声明是通过"<>"实现

> 约定泛型可以使用单个大写字母来表示 K E T V 等

1. 泛型类

2. 泛型方法

   ```java
   public class Demo07<K, V> {
       /**
        * 普通方法 可以使用 类中定义的泛型
        * @param k
        * @param v
        * @return
        */
       public K method1(K k, V v) {
           return (K) null;
       }
   
       /**
        * 普通方法 使用方法中定义的泛型
        * @param t
        * @param v
        * @param <T>
        * @return
        */
       public <T> T method2(T t, V v) {
           return (T) null;
       }
   
       /**
        * 在静态方法中我们没法使用 类中定义的泛型
        * @param <K>
        * @return
        */
       public static <K> K method3() {
           return null;
       }
   }
   ```

3. 泛型接口

   ```java
   public interface CalGeneric <T> {
       T add(T a, T b);
   
       T sub(T a, T b);
   
       T mul(T a, T b);
   
       T div(T a, T b);
   }
   ```

   

## 反射

### 1. 反射定义

​		反向探知，在程序运行过程中动态的获取类的相关属性

> 这种动态获取类的类容以及动态调用对象的方法和属性的机制就叫做JAVA的反射机制

反射的优缺点

> 优点
>
> ​	增加程序的灵活性，避免固有逻辑写死到程序中
>
> ​	代码相对简洁，可以提高程序的复用性
>
> 缺点
>
> ​	相比直接调用，反射有比较大的性能开销
>
> ​	内部暴露和安全隐患

### 2. 反射的操作

1. 基本操作

   * 获取类对象的四种方式

     ```java
     // 获取类对象的四种方式
     Class<User> clazz1 = User.class;
     Class<?> clazz2 = Class.forName("com.zw.example.fs.User");
     Class<? extends User> clazz3 = new User().getClass();
     Class<?> clazz4 = Demo03.class.getClassLoader().loadClass("com.zw.example.fs.User");
     ```

   * 基本信息操作

     ```java
     System.out.println(clazz1.getModifiers());
     System.out.println(clazz1.getPackage());
     System.out.println(clazz1.getName());
     System.out.println(clazz1.getSuperclass());
     System.out.println(clazz1.getClassLoader());
     System.out.println(clazz1.getSimpleName());
     System.out.println(clazz1.getInterfaces());
     System.out.println(clazz1.getAnnotations());
     ```

   * 字段操作

     ```java
     Class<User> userClass = User.class;
     User user = userClass.newInstance();
     
     // 获取类型中定义的字段，公有字段以及父类中公有的字段
     Field[] fields1 = userClass.getFields();
     for (Field f : fields1) {
       System.out.println(f.getModifiers() + " " + f.getName());
     }
     
     System.out.println("----------------------------");
     
     // 可以获取私有字段，只能获取当前类中的字段
     Field[] fields2 = userClass.getDeclaredFields();
     for (Field f : fields2) {
       System.out.println(f.getModifiers() + " " + f.getName());
     }
     
     System.out.println("----------------------------");
     
     // 获取name字段对应的Field
     Field nameField = userClass.getDeclaredField("name");
     // 如果要修改私有属性信息，需要放开权限
     nameField.setAccessible(true);
     nameField.set(user, "1111");
     System.out.println(user.getName());
     
     System.out.println("----------------------------");
     
     // 静态属性赋值
     Field addressField = userClass.getDeclaredField("address");
     addressField.set(null, "2222");
     System.out.println(User.address);
     ```

   * 方法操作

     ```java
     Class<User> userClass = User.class;
     User user = userClass.newInstance();
     // 可以获取当前类以及父类中的所有的公有的方法
     Method[] methods1 = userClass.getMethods();
     for (Method m : methods1) {
       System.out.println(m.getModifiers() + " " + m.getName());
     }
     System.out.println("--------------------");
     // 可以获取私有方法，只能获取当前类中的方法
     Method[] methods2 = userClass.getDeclaredMethods();
     for (Method m : methods2) {
       System.out.println(m.getModifiers() + " " + m.getName());
     }
     System.out.println("--------------------");
     Method jumpMethod = userClass.getDeclaredMethod("jump");
     // 放开私有方法的调用权限
     jumpMethod.setAccessible(true);
     jumpMethod.invoke(user);
     System.out.println("--------------------");
     // 静态方法调用
     Method sayMethod = userClass.getDeclaredMethod("say", String.class);
     sayMethod.invoke(null, "666");
     ```

   * 构造器操作

     ```java
     Class<User> userClass = User.class;
     // 获取所有的公有的构造器
     Constructor<?>[] constructors1 = userClass.getConstructors();
     for (Constructor c : constructors1) {
       System.out.println(c.getModifiers() + " " + c.getName());
     }
     System.out.println("-------------------");
     // 获取所有的构造器
     Constructor<?>[] constructors2 = userClass.getDeclaredConstructors();
     for (Constructor c : constructors2) {
       System.out.println(c.getModifiers() + " " + c.getName());
     }
     System.out.println("-------------------");
     // 1. 直接通过newInstance创建对象
     User user = userClass.newInstance();
     // 2. 获取对应的Construction对象获取实例
     Constructor<User> constructor1 = userClass.getDeclaredConstructor(String.class, String.class);
     // 私有的构造器调用放开权限
     constructor1.setAccessible(true);
     constructor1.newInstance("gg", "男");
     ```

### 3. 单例的漏洞

产生原因是：反射可以调用私有构造器造成的

解决方案：在私有构造器中加入逻辑判断结合`RuntimeException`处理即可

```java
public class PersonSingle {
    private static PersonSingle instance;

    private PersonSingle() {
        if(instance != null) {
            throw new RuntimeException("不允许重复创建");
        }
    }

    public static PersonSingle getInstance() {
        if (instance == null) {
            instance = new PersonSingle();
        }
        return instance;
    }
}
```

### 4. 反射使用场景

1. jdbc封装

2. SpringIOC

3. jdbcTemplate

4. Mybatis

   ...

### 5.反射的应用 SpringIOC

IOC 控制反转 就是一种设计思想，容器 管理对象



## 注解

### 1.JDK 常用预定义注解

```java
@Override                 // 编译检查
@Deprecated               // 表示方法弃用
@SuppressWarnings("all")  // 抑制警告
```

### 2.自定义注解

格式(注解本质就是接口)

 ```java
public @interface MyAnn {
	String name();
  int age() default 18;
}
 ```

反编译后的内容

```java
public interface Name extens java.lang.annotation.Annotation {
}
```

属性：在接口中定义的抽象方法

> 返回结果必须是如下类型
>
> 1. 基本数据类型
> 2. String类型
> 3. 枚举类型
> 4. 注解
> 5. 以上类型的数组

属性赋值注意点：

> 1. 如果定义的属性时，使用default关键字给属性设置默认初始值，可以在使用注解时不赋值。
>
> 2. 如果只有一个属性需要赋值，而且该属性名称是value，那么在赋值时可以省略 `value=`。
> 3. 数组赋值的时候，值使用`{}`包裹，如果数组中只有一个值，那么`{}`可以省略。

### 3.元注解

JDK中给我们提供的4个注解

> 1. @Target: 描述当前注解能够作用的位置
>    * ElementType.TYPE: 可以作用在类上
>    * ElementType.METHOD: 可以作用在方法上
>    * ElementType.FIELD: 可以做用户在成员变量上
> 2. @Retemtion: 描述注解被保留到的阶段
>    * SOURCE < CLASS < RUNTIME
>    * SOURCE: 表示当前注解只在代码阶段有效
>    * CLASS: 表示该注解会被保留到字节码阶段
>    * RUNTIME: 表示该注解会被保留到运行阶段
>    * 自定义注解：RetentionPolicy.RUNTIME
> 3. @Documented: 描述注解是否被抽取到JavaDocAPI中
> 4. @Inherited: 描述注解是否可以被子类继承