

权限修饰符：public        protected     默认不写    private

特征修饰符：abstract         final           static           nativ等等

> private：本类。 
>
> 默认：本包
>
> protected：本包+子类(子类对象调）
>
> public：所有

类的成员：

* 属性：权限  特征  类型  名字  [=赋值]
* 方法：权限  特征  返回类型  名字(参数)  异常  [{方法体}]
* 构造函数：权限  名字(参数)  异常  {方法体}
* 块：方法体

类：`public` 或 `不写`

1. 普通类：public class Person{ ... }
2. 本包私有类： class Person{ ... }
3. 抽象类：public abstract class Person{ 属性; ...可以有0或多抽象方法...普通方法...静态方法...块... }  
   * 可以有构造函数，不能实例化。可以有块。
   * 没有抽象方法，都是具体方法，也可以定义为抽象类，抽象类不能实例化，根据需求设定即可
4. 接口：public interface Box{ 属性都是静态常量 - 默认public static final( - 没有实例字段)；只有抽象方法} 
   * 接口不是类。不能有构造函数，不能实例化。
   * 不能有块。
5. 枚举类：public enum Day{ monday, tuesday }

> 1）**接口**不能**有构造**方法，抽象类可以**有**。 2）**接口**不能**有**方法体，抽象类可以**有**。 3）**接口**只有抽象方法，1.8后可以**有**静态方法（只能调静态字段）。抽象类可以**有**静态方法和普通方法和抽象方法，数量无限制。 4）在**接口**中凡是变量必须是public static final，而在抽象类中没有要求。

属性：只能声明 或 声明时赋值。不能写赋值语句。

1. 普通属性：public/private/默认/protected Computer[ ] computers;    这个属性是一个数组。

2. 静态属性：private static int nextId;  属于类的 ，不属于任何一个对象，可改变，private只能类内部访问。

3. 静态常量：public static final String name = "Static Name";   属于类。final属性不能被改。静态常量建议public。

   * final属性：

     ```java
     class Demo{
        final int i = 1; //①final属性: 声明时赋值。
        final int x;
        public Demo(int i){  //②final属性: 声明时不赋值，但通过初始化块 或 构造函数传参来初始化赋值。
           this.i = i;
        }
        final static int n = 3;//③final static属性: 必须声明时赋值。【这就是常量】
     }
     ```

     因为属性在类加载时(静态属性)和对象创建时(普通属性)会被赋予默认值。必须在赋予默认值之前(通过代码块或构造函数)来给final属性赋值，否则这个属性就没有意义。

4. 抽象类的属性：同上。

5. 接口的属性：String name; 默认都是public static final公有静态常量。

方法：

1. 静态方法：public static double random(){  ...  }  只能访问静态变量，不能访问对象变量。（在静态区加载，但是不默认执行，调用时才执行）静态方法可以直接通过类来调用。
2. final方法：public final boolean testTrue(){  ...  }  不能被子类重写。

3. 抽象方法：public abstract void getDescription();  必须public。没有方法体，必须被子类实现。或子类也是抽象类，保留抽象方法。
4. native方法：public native clone();   方法体内容由其他语言写成，没有java方法体。

构造函数：

1. 普通类的构造函数：4权限修饰符都可用
2. 抽象类的构造函数：4权限符都可（但是不能构造对象，只能给子类用）
3. 接口没有构造函数。

块：`static` 或 `无`

1. 普通块。默认在执行构造函数前执行。
2. static块。静态块，类加载时就执行。所以是先执行静态块（静态块可访问静态属性），再执行普通块。

变量：

1. final变量：final int a。在方法内部不能被改变。





##### 二、java基础夯实

* if ( 逻辑 - boolean ){ ... }

* switch( 值 - int/char/enum/String){ ... }
  * 记得break - 想起break，记得带标签的break —— 在循环语句前：cat: for(...){ ...  break cat; }
  * 有事也可以利用下漏，所种结果，执行同一种操作，或逐步增加操作 —— 就不要加break。

* 在java的调用机制中：调用属性，不需要跟括号；调用方法，都需要跟括号。
  * java的一切都在类里，一切东西，都是类，一切都在类里面。
  * 凡是要用的，都要new对象——或类自己new，你调用类创建好的对象（单例模式/枚举类）。
  * java里的执行只有4种：创建、赋值，调用方法+调用属性，for switch 数组等基本循环判断存储模式。
* 只要new就产生了一个新空间。

* **java的核心基础：**

  * 值存在哪里？变量(空间)——有的直接存在变量空间，有的存在变量空间所存的地址空间里（引用类型）。

    * 值的类型和存储地点：
    * 基本数据类型8个：byte short int long，double float，boolean，char ----> 存在自己类型的变量里（注意变量的命名规则）
    * 连续多个值或字符的存储：引用类型 ----> String和数组。`数组：int[ ] a = new int[5];`  同样注意变量名的命名规则。
    * 引用类型5个：数组[]、类(抽象类)class、接口interface、枚举enum、注解@interface

  * 值怎么改变：赋值(=)。

  * 值怎么根据我们的逻辑目的改变？判断语句、循环语句。

    * 判断语句：if，if else，if else if else(单分支-->多分支)。switch(多分支)。
    * 循环语句：for，while。

    * 补充知识：break和continue，带标签的break，for each。

  * ----------------------------------面向对象的核心思想----------------------------------

  * 类。封装，一切都在类里，执行都在方法里。

    * 类的组成部分：属性，构造函数，方法，块
    * 修饰符：权限修饰符public proteced 默认不写 private，特征修饰符static final abstract 
    * （类只有public和不写）（abstract class是抽象类）（interface是接口，也是public和不写）static类的  final不能改

  * 继承：单继承。子类构造对象时，会默认先构造一个自己的父类对象（单独给自己服务），再完成自己的构造。子类可以直接使用父类的属性super.name、方法super.getName()、和构造函数super(,,)。
    * super和this的用法（this用于解决形参名与属性名重名问题）。
    * 对象的创建、类的加载顺序和过程。
  * 多态：抽象类、父类、接口的变量，可以指代具体子类的对象。实现传同一个参数进去，走不同执行方法的效果。
  * 内部类。内存管理机制。

* 什么是聚合关系？

  * ```java
    public class Test{
       public Person p = new Person(); //聚合关系
    }
    ```

  * is-a 继承 实现

  * has-a 聚合

  * use-a

##### 三、java核心概念

1. 多态：父类、抽象类、接口的对象，可以引用更加子类对象。（一个抽象的类的变量，可以引用具体的子类的对象）
   * Person p = new Student();
   * 其中抽象类和接口，都不能有对象。父类可以有。

2. 面向对象的三大特性：继承、封装、多态

3. 接口没有父类。

   > 所以接口是干嘛用的？
   >
   > ① Java core的说法是，你要想使用一些方法，必须实现某个接口。比如你想用.sort()方法，必须实现Comparable接口里定义的compareTo()方法。
   >
   > ② 接口定义了一系列规则(需求)，实现类必须实现里面的接口。于是可以用接口对象 实现多态。





##### 四、重复有益的知识点：

1. 只要new就会产生一个新空间（对内存stack）

2. .equals()方法默认在Object类中的效果是：return this==obj;  也就是说equals()方法默认等同于`==`号。

   * `==`比较的是里面存的**值**。**凡是对象**变量，**存的都是地址**。

   > == 和 equals的区别：
   >
   > * == 可以比较基本数据类型，也可以比较引用数据类型（== 比较变量中存储的内容）。
   >
   > * equals()方法默认效果是==，此方法经常被重写。Integer类重写了此方法，所以`Integer对象.equals(obj)`比的是值。

   

