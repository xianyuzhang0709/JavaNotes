# 类之间的 关系：

* A   is-a   B   （泛化）继承  实现   inheritance

* A  has-a B   （包含） 组合  聚合   关联  composition

* A  use-a B   （依赖） 依赖（need a）

### 一、继承 extends: is-a

![image-20201220102757030](DUYI_java_ii_Class.assets/image-20201220102757030.png)

1. 子类对象可以调用父类的（**public**和**protected**）的属性和方法。

   * 构造方法不算子类继承过来的，只是在子类产生对象时，默认调用父类的构造方法。
   * 程序块，在调用父构造方法之前，自动调用了父类块。

2. 子类可添加自己的方法和属性。

3. 子类可以重写（override）父类方法。

4. 所有的类都继承了Object类。

5. java的继承是**单继承**，每个类只能有一个继承的父类，父类可以有一个祖父类。（extends后面只能跟一个类）—— 为了类的安全。

   * 传递——实现多继承
   * 多实现——实现多继承

6. 继承在内存中的存储形式

   * 当你创建了一个Person p = new Person()，你会发现，Person的父类Animal的构造方法也走了一遍。
   * 1. 加载类模板的过程： Object类 Animal类 Person类 —— 三个类的模型都加载，然后三个类是继承关系。
   * 2. new Person在堆内存中创建对象。并且会执行一遍父类的构造方法（但不会产生一个父对象）——总之就是会加载一遍父类的构造方法。这里面加载出来的东西只为子对象服务。（其实就是一个子类，没有产生父类的任何东西）（所有都是子类的）

   * ![image-20201219215033818](DUYI_java_ii_Class.assets/image-20201219215033818.png)

   * 当你构造了一个子类对象，同时也会构造出一个父类对象。相当于在你的构造函数第一行写了默认的隐藏的super();

     * 总之是需要调用父类的构造方法，才能调用父类的所有方法。

   * 例子：

   * ```java
     class Animal{
        public Animal(){  System.out.println("Animal无参构造方法");  }
        public	void eat(){  System.out.println("Animal吃");  }
        public void sleep(){ this.eat(); System.out.println("Animal睡");  }
     }
     class Person extends Animal{
        public Person(){  System.out.println("Person无参构造方法");  }
        public void eat(){  System.out.println("人吃东西，香");  }
     }
     public class Test{
        public static void main(String[] args){
           Person p = new Person();  //这里执行了: Animal无参构造方法+Person无参构造方法
           
           p.sleep();  //这里执行了: Person的eat和Animal里继承的sleep ---> 调用的不是Animal的eat
                       //如果子类重写了eat方法，那么this只能调到子类的eat方法。想调父类的eat，要用super
        }
     }
     ```

7. **this** 代替的是**当前**调用方法属性时的**对象**。不一定是当前类的对象 —— 可能是子类的对象 —— 如果子类对象有重写方法，在父类中方法调用其他方法时，优先找子类同名方法

   **super** 代替**当前**执行方法时的对象的**父类**的**对象**（其实不是对象，反正是父类的东西）。

   * 都能调用一般属性和一般方法
   * 可以放在类成员的任意位置（属性、方法、构造、块）
     * 一般方法中可以来回调用，但会有Error
   * 可以在构造方法中调用另一个构造方法（必须在第一行）
     * 构造方法中来回调用，写就不好用。因为它们都要在第一行。。。（不懂 0,0）

#### 0. 所有类的父类：Object类

java.lang包。

方法：

1. **hashCode()** : 将对象在内存中的地址经过计算得到一个int整数。

   * ```java
     public nativ hashCode(); // ---> native表示这部分代码是用c++写的，java代码已经到头了。
     ```

2. **equals()** :  用来比较两个对象的内容

   * ```java
     public boolean equals(Object obj){  return (this==obj);  }
     ```

   * 默认效果是 == 

     * == 比较基本类型，比的是**值**。
     * == 比较引用类型，比较**地址**。

   * equals建议重写

3. **toString()** :  打印输出时将对象变成String字符串

   * ```java
     public String toString(){  return this.getClass().getName()+"@"+Integer.toHexString(this.hashCode());  }
     ```

   * Return：类全名+@+int整数（转换成了十六进制）

4. **getClass()** :  获取对象对应类的类映射（反射）

5. **wait()** :  线程进入挂起等待状态  

   * 存在方法**重载**：有三个带不同参数的wait()方法

6. **notify()** :  线程唤醒

7. **notifyAll()** :  唤醒所有

8. **finalize()** :  protected方法，在对象被GC回收时，默认调用执行的方法。（析构函数）

   * ```java
     protected void finalize(){}
     ```

   * 什么都没做

   * final finally finalize区别

9. **clone()** :  protected方法，为了克隆对象。

#### 1. Override vs Overload

![image-20201219204408707](DUYI_java_ii_Class.assets/image-20201219204408707.png)

权限符：public > protected > 默认不写 > private

* 子类的权限符范围可以>=父类的

#### 2. 继承写法用法都不难，问题是什么时候用继承？内存原理了解了？super和this的特点？

#### n. 包

```java
package com.horstman.corejava;
```

package只能有一个，import可以写多个。package写在最前。

### 二、包含 has-a (组合 聚合 关联)

组合：人和大脑、人和心脏（整体和部分不可分割，要出现都出现，要消亡都消亡）

聚合：汽车和轮子  电脑和主板（整体和部分  在创建时可以分开的）

关联：人又汽车  人有电脑（可以分割，后来在一起）

### 三、依赖 use-a 

Eg：屠夫 杀 猪。

因为一件事联系在一起，事情完成，关系结束。

java程序体现：**一个类的方法中使用到另一个类的对象。**形式：

* 在方法中传递参数
* 在方法中自己创建

### 四、设计类的原则：高内聚，低耦合

耦合度：最紧密是    继承（实现）> 包含 > 依赖

例子1：学生在机房使用电脑

* 有一个机房
* 有一台电脑  电脑有开机/关机状态  电脑被打开  电脑被使用中  电脑被关闭
* 有一个学生
* 学生进入机房使用电脑

扩展：

* 机房内5台电脑
* 学生进入机房选一太关闭的电脑使用
* 学生5个，陆续进入机房

例子2：汽车测速器





![image-20201220112717652](DUYI_java_ii_Class.assets/image-20201220112717652.png)

类，有权限修饰符，也可能有特征修饰符final

# 修饰符

![image-20201220113025912](DUYI_java_ii_Class.assets/image-20201220113025912.png)

### 一、 权限修饰符: public / protected / 默认不写 / private

|                                                 |             权限修饰符              |     特征修饰符      |    特征修饰符     |
| :---------------------------------------------: | :---------------------------------: | :-----------------: | :---------------: |
|                     **类**                      |            public / 不写            | final 本类不可继承  | static 静态内部类 |
|               (类的) **构造方法**               | public / protected / 不写 / private |       （无）        |      （无）       |
|                 (类的) **方法**                 | public / protected / 不写 / private |   final 不可重写    |  static 静态方法  |
|                (类的) **程序块**                |               （无）                |    static 静态块    |      （无）       |
|                 (类的)**属性**                  |          public / private           | final 不可改+必赋值 |  static 静态属性  |
| (方法的) **变量**<br />- 存在栈内存的临时空间 - |               （无）                | final 方法内不可改  |      （无）       |

* 静态方法只能调用静态变量。不能调用对象变量。因为静态的意思是，不需要对象就可以执行。
* 属性：静态属性存在方法区静态空间；普通属性，跟随对象，在对象空间内（堆内存）。
* 变量：在栈内存。
* final：值不可改。但是如果值是一个对象的引用，可以改对象本身的值。

下图：权限修饰符 所表示的 范围

|  权限修饰符   |          | 范围（谁可以访问你？）                    |
| :-----------: | :------: | ----------------------------------------- |
|  **public**   |   共有   | 本类 本包 子类 任意类里(创建对象就可访问) |
| **protected** | 包和子类 | 本类 本包 子类(↓)                         |
| **默认不写**  |  包私有  | 本类 本包                                 |
|  **private**  | 本类私有 | 本类                                      |

**本包**：严格地在同一个包里，不能是在同大包不同小包。

**protected**：在子类范围内，通过子类对象，访问父类的受保护方法，可以。

* 在子类内，创建父类对象访问父的protected方法，也不行。
* 在（父和子类的）外部，通过子类对象，访问父类protected方法，不行。

### 二、特征修饰符: final / static / abstract / nativ ...

#### 1. final

* **final 类**：不能被子类继承 —— 通常是定义好的工具类，比如：Math类、Scanner类、Integer类、String类。

* **final 方法**：不能被子类重写。

* **final 属性**：属性即便没赋值，也有默认值，所以 ①要么声明时赋初值 ②要么声明时不赋值，在代码块或构造函数中赋值。

* **final 变量**：变量声明后，只有一次赋值机会，一旦赋值不能再改变 —— 相当于常量。

  * ```java
    public void testNum(final int[] a){....}  //也可以，表示a在方法内不能被改变
    ```

> final 属性 和 final 变量：
>
> ①一旦赋值，不再能修改。      ②变量或属性：如果是基本类型，则不能改；如果是引用类型，地址不能改，但值可以改。

#### 2. static 静态

静态元素，在创建类时就完成了加载和初始化。它**属于类**，不属于任何一个对象。可以通过类名字直接访问，也可以通过对象直接访问。

静态成员之间可以互相访问。静态成员不可以访问一般方法（因为你不知道找哪个对象的方法）。也不能用this和super（因为这俩指代对象）

* 静态常量使用场景：private static final 属性 = 0;

内存管理：栈内存用完就回收，对内存用GC回收，静态元素区GC无法管理。静态元素常驻内存。

![image-20201220151143311](DUYI_java_ii_Class.assets/image-20201220151143311.png)

* **static 属性**：
* **static 方法**：
* **static 块**：(静态块)
* **static class**：(内部类)

```java

```



### 三、java面向对象三大特性：继承 封装 多态 （第四：抽象）

private : **封装** —— 把一些数据和方法进行包装

* 目的：封装执行过程，保护数据和执行过程，隐藏执行细节，增强复用性

所以：

* 属性，全部private
* public方法，提供功能
* 所有属性的访问和修改 --->
  *  age ---> setAge()和getAge()方法来实现

Spring： IOC——对象的控制权是别人的。向别人要，别人帮你创造对象。DI依赖注入——帮你赋值。

### 四、设计模式23种之一：单例模式singleton

设计模式是通用的代码书写方案，确保代码可读性、复用性、可靠性、可扩展性

三类：

1. 创建型模式 5 ---> 用于解决对象创建的过程

   单例模式   工厂方法模式   抽象工厂模式   创建者模式   原型模式

2. 结构型模式 7 ---> 把类或对象通过某种形式结合在一起，构成某种复杂但更合理的结构

   适配器模式   装饰者模式   代理模式  外观模式   桥接模式  组合模式   享元模式

3. 行为型模式 11 ---> 解决类或对象之间的交互，合理优化类或对象之间的关系

   观察者模式   模板模式   策略模式   责任链模式  解析器模式  迭代子模式  命令模式  状态模式  备忘录模式  访问者模式  中介者模式

#### 1. 单例模式

一个类，我们希望**它只会创建一个对象**。

把这一个对象直接创建在类的属性里：

```java
class SingleTon{
		private SingleTon single = new SingleTon();
}
```

-----> 这会导致StackOverflowError栈内存溢出。堆内存溢出是OutOfMemory。

因为创建对象时执行构造方法 ---> 在栈内存执行 ---> 执行时又要new一个新对象，执行新的构造方法 ----> 最终导致栈内存溢出（栈小堆大，栈先溢出）。

![image-20201220182804470](DUYI_java_ii_Class.assets/image-20201220182804470.png)

把对象创建放在静态属性里：静态对象只加载一次。

```java
class SingleTon{
  //把唯一的对象，创建在static属性中
  private static SingleTon single = new SingleTon();  //立即加载: 饿汉式
  
  //让构造函数私有，这样就不能随便构造新对象
  private SingleTon(){}
  
  //写一个获得本对象的public静态方法: --> 本方法通过类名即可访问，不需要对象
  public static SingleTon getSingleTon(){  //单例模式规约：get方法名字可以是 ①get类名 ②newInstance
     return single;
  }
}
```

于是就需要一个静态方法（属于类的方法，直接用类名就可以访问，不需要非要通过对象访问），来让用户访问到这个唯一对象——却不能随意更改它。

访问这个唯一的对象：

```java
class Test{
  public static void main(String[] agrs){}
  	//SingleTon s = SingleTon.single; 如果类里的属性是public，可以这么访问
  	SingleTon s = SingleTon.getSingleTon();//得到了single的地址引用，single不能被改变，只能被访问
}
```

> 总结单例模式实现方法：
>
> 1. 把构造方法私有。
> 2. 私有、静态  的属性 = new 类(); 
>    * 唯一对象生成在类的静态属性里（独此一份，且不会溢出，因为它再怎么内部反复调用自己，也都在指代它自己）
> 3. 共有、静态  的方法，返回该对象。 提供该对象的访问功能。

单例模式：

* 饿汉式（立即加载）对象启动就加在 --- 我们刚写的就是饿汉式
  * 好：不会空指针异常（对象还没有，就要用）。
  * 坏：服务器承载压力过大
* 懒汉式（延迟加载）对象什么时候用才加载
  * 好：可能操作不好，产生问题导致异常
  * 坏：服务器压力不大，不会浪费空间
* 生命周期托管（单例对象由别人帮助我们处理）对象加载过程交给别人

饿汉式：类加载时，就new了这个对象。`private static SingleTon single = new SingleTon();`

懒汉式：类加载时，不创建对象。在getSingleTon()方法里才创建。

```java
class SingleTon{   //懒汉式 -- 延迟加载
   private static single;
   private SingleTon(){}
   public static SingleTon getSingleTon(){
     if(single==null){
       single = new SingleTon();
     }
     return single;
   }
}
```



#### 2. 缺省适配器模式Adapter

有接口的好处是统一管理。可是如果接口要增加方法，所有子类也必须增加方法。

我们之前写的LInkedBox类是对接口Box的实现。所以用的是implements。

而我们现在要加一个二者之间的**抽象类：**这就是适配器

1. **把不太重要的方法削减出去（它自己具体化），让一些子类去找合适自己的用。**
2. 把子类里重复的代码放在这个适配器抽象类里去写，子类直接调用父类方法即可。

```java
public abstract class AbstractBox implements Box{
    //接口定义的抽象方法继续保留
    public boolean add(int element);
    public int remove(int index);
    public int get(int index);
    public int size();
    
    //自己定义更多方法 让子类根据需求自行实现这部分内容  子类extends这个适配器
    public void add(int index, int element){
      throw new 自定义Exception;
    }
    public void addAll(Box){
      throw new 自定义Exception;
    }
}
```

这个抽象类实现了接口interface，并且另外增加了两个方法。子类则extends这个类即可。

子类可以实现接口，但是如果接口要增加方法，就必须让子类都实现这些方法。适配器的作用就是，它实现接口，而让子类去继承它，那么子类已实现接口前面的需求，而后面新增的功能，都在适配器这个父类里——它可以根据需要进行重写，或者不理睬（反正不重写就不能用，可以调，但不能用，一调用就只有异常报出，没有别的功能实现）。

而这两个方法：

* 子类可以不写，如果不写又想直接调用，会抛出异常，所以  想用就必须重写。
* 可以不写，因为父类已经把这两个类设置为具体方法，而不是抽象的。



### 五、特征修饰符：final static abstract native ...

#### n. 类加载的顺序过程

```java
class Animal{
   private String test = "AnimalTest";
   private static String staticTest = "AnimalStaticTest";
   public Animal(){
      System.out.println("Animal无参数构造方法");
   }
   {
      this.test();//普通块调用普通方法
      System.out.println("Animal普通块");
   }
   static{ 
      staticTest();    //静态元素可以访问静态元素，但不可访问普通元素。也可以写为: Animal.staticTest();
      System.out.println("Animal静态块" + staticTest);  //这里调用了静态方法和静态属性
   }
   public void test(){
      System.out.println("Animal普通方法");
   }
   public static void staticTest(){
      System.out.println("Animal静态方法");
   }
}

class Person extends Animal{
   //子类可以有跟父类重名的属性，这不叫重写。如果有就用自己的，没有就用父的。
   private String test = "PersonTest";
   private static String staticTest = "PersonStaticTest";
   public Person(){
      System.out.println("Person无参数构造方法");
   }
   {
      this.testP();
      System.out.println("Person普通块"+test);
   }
   static{ 
      staticTest();
      System.out.println("Person静态块"+staticTest);
   }
   public void testP(){
      System.out.println("Person普通方法");
   }
   public static void staticTest(){
      System.out.println("Person静态方法");
   }
}

public class Test{
   public static void main(String[] args){
		  new Person();//这里发生了什么？创建对象时发生了什么？
   }
}
//结果: 先出静态，后出非静态。先出父，后出子。
```

对象创建之前，类先加载：

1. 加载类模板：先加载父类，后加载子类： (先把东西摆放好) 

   * 加载父类静态成员：
     * 方法区：Animal类模板 { 普通属性、普通方法、普通块、构造函数 } 
     * 静态区：Animal静态空间 { 静态属性、静态方法、静态块}                     (按顺序)
     * 然后**执行父类静态块**

   * 加载子类静态成员：
     * 方法区：Person类模板 { 普通属性、普通方法、普通块、构造函数 }
     * 静态区：Person静态空间 { 静态属性、静态方法、静态块}
     * 然后**执行子类静态块**

2. 创建对象空间：

   * 加载父类的非静态成员：
     * 加载Animal类的普通属性、普通方法、普通块、构造函数                     （按顺序）
       * 普通方法和构造函数并不存储在这里，这里只记录了类模板中对应方法的地址
     * **执行父类普通块**，**执行父类构造函数**

   * 加载子类非静态成员：
     * 加载Person类的普通属性、普通方法、普通块、构造函数
     * **执行子类普通块**，**执行子类构造函数**

3. 把对象空间的地址交给 接收它的变量

```java
//结果:
Animal静态方法
Animal静态块AnimalStaticTest  //Animal 静态方法 + 静态块 + 静态属性
Person静态方法
Person静态块PersonStaticTest  //Person 静态方法 + 静态块 + 静态属性
Animal普通方法
Animal普通块                  //Animal 普通块(调用普通方法)
Animal无参数构造方法           //---Animal构造---
Person普通方法
Person普通块PersonTest        //Person 普通块(调用普通方法)
Person无参数构造方法           //---Person构造---
```

![image-20201220213029943](DUYI_java_ii_Class.assets/image-20201220213029943.png)

**（图：Person p = new Person(); 的加载过程 - Person的父类Animal）**

```java
//--第3步完--
Animal静态方法
Animal静态块AnimalStaticTest 
//--第6步完--
Person静态方法
Person静态块PersonStaticTest 
//--第9步完--
Animal普通方法
Animal普通块             
//--第9步完--
Animal无参数构造方法          
//--第11步完--
Person普通方法             
Person普通块PersonTest   
//--第11步完--
Person无参数构造方法             
```

针对第9和第11步：逐步加载，一起执行。

这部分是虚拟机的工作原理。以上依然很多不准确。

#### 3. abstract 抽象的 (只有概念，没有具体执行)

**抽象类：abstract修饰。**

**抽象方法：abstract修饰。只有方法结构，没有执行体。**

* 抽象类不是必须有抽象方法。
* 抽象方法可以放在 抽象类(abstract class) 或 接口(interface) 中。
* 普通类不允许含有抽象方法。

```java
public abstract class Animal{
   public abstract void eat();  //抽象类没有执行体
}
```

##### 3.1 抽象类

通常用来描述事物，但还不够具体。

![image-20201220220438450](DUYI_java_ii_Class.assets/image-20201220220438450.png)

![image-20201220224130949](DUYI_java_ii_Class.assets/image-20201220224130949.png)

![image-20201220224427828](DUYI_java_ii_Class.assets/image-20201220224427828.png)

```java
public interface Test{}
```

##### 3.2 接口、抽象类、普通类之间的关系

![image-20201220224733316](DUYI_java_ii_Class.assets/image-20201220224733316.png)

![image-20201220225049479](DUYI_java_ii_Class.assets/image-20201220225049479.png)

##### 3.3 抽象类和接口的知识回顾

![image-20201221130456037](DUYI_java_ii_Class.assets/image-20201221130456037.png)

![image-20201221130832111](/Users/zhangxianyu/Java_Notes/DUYI_java_ii_Class.assets/image-20201221130832111.png)

##### 3.4 案例

![image-20201221142834689](DUYI_java_ii_Class.assets/image-20201221142834689.png)

数据结构之链式结构：

* 单向链表 A -> B -> C -> ...
* 双向链表 A <-> B <-> C <-> ...
* 环形链表 

![image-20201221143104889](DUYI_java_ii_Class.assets/image-20201221143104889.png)

### 六、多态

![image-20201221202216501](DUYI_java_ii_Class.assets/image-20201221202216501.png)

5. 这里的意思是：

   * **Person类型的变量p，指向一个Teacher类的对象。**

   * **子类对象，可以赋值给超类变量**。但是超类对象 引用给 子类变量，会导致方法调用时出错。

6. 强制向下转型时，可能会造成运行时异常（ClassCastException类造型异常）

   * 比如：Student s = (Student) o;  //编译没问题，但是运行会出问题
   * 必须是父子类关系才可以造型

7. 如果想避免异常，可以进行**instanceof判断**。

   * 用法：**对象 instanceof 类 --> 返回结果为true/false**

![image-20201221203750739](DUYI_java_ii_Class.assets/image-20201221203750739.png)

* ---------------------------------**Student s = (Student) o;**  //编译没问题，但是运行时异常 —— ClassCastException类造型异常

### 七、知识回顾及补充

#### 知识回顾：适配器和多态

> 知识回顾：适配器和多态
>
> 适配器：解决一个接口定义了好多方法的问题
>
> 适配器通常是一个抽象类，implements接口，并添加了某些具体方法（方法内抛出异常）
>
> 这样它就是一个特殊的接口，接口定义的抽象方法方法子类必须重写。
>
> 
>
> 多态：指一个对象变量可以指代不同的类对象，表现出不同的形式。
>
> 多态首先必须有父子关系。父的变量，指代不同的子对象。
>
> * People p = new Teacher(); （向上转型自动进行）
>
> 此变量p只能调用父定义的方法和属性。属性调父的，方法调最靠近本质的子的。
>
> 向下转型，叫造型。需要考虑转型类型与实际类型不匹配的问题（ClassCastingException）
>
> * 可以用【 p  instanceof  Student 】来判断是否可以造型





#### Java Core 知识补充：**构造器**

> Java Core 知识补充：**构造器**
>
> **仅当**类中**没有任何构造器的时候**，系统才会**默认给你一个无参数的构造器**。一旦你定义了构造器，就不能使用无参构造来创建对象。
>
> 父子类：
>
> 1. 父无构造器，子无构造器。系统：给二者都提供无参构造器，并且子构造器里第一行默认调父的构造器。
>
>    ---> 创建一个子类对象时，先先构建父对象字段部分（先执行父构造器），再构建子对象字段部分（再执行子构造器）。
>
> 2. 父无构造器，子有参构造器。系统：给父一个无参构造器，子构造器第一行调用父无参构造器。
>
>    --->创建一个子类对象时，先父部分构建，再子部分构建。
>
> 3. 父有无参构造器，子无构造器。系统：给子一个无参构造器，子构造器第一行调用父无参构造器。
>
>    --->创建一个子类对象时，先父部分构建，再子部分构建。
>
> 4. 父有有参数构造器。系统：子必须有一个构造器 匹配父构造器matching super constructor。
>
>    ---> 子构造器中，要先在第一行调用父构造器并传入属性：public Student(String name, String major){ **super(name);**  this.major=major; }  之后再初始化自己的属性。
>
>    * 这样的效果是：父类有所有子类的共同字段name，并有构建赋值能力（抽象类的构造器，纯粹只给子类构建器用，抽象类不能有实例），并有获得字段的能力——getName方法（所有子类只能通过这个公有方法来获得[这个唯一为自己服务的]父对象的private name字段。为什么不用protected？因为这样子类可以直接用这个字段了，也可以直接改 —— 其实也行）
>    * 另一种理解是，protected的话，父类的属性和父类的方法，子类对象都可以直接调用。this.name(即使子类里没有name字段)  this.fatherProtectedMethod()  
>    * 效果是：子类只有各自独有的属性，和独有的方法，以及重写的父类的方法（减少重复代码）。如果是抽象类的子类，那么还有抽象类定义的抽象方法的具体化方法（其实也是一种重写）。



那么适配器是什么？

---> 是一个抽象类，接口的要求还在那里，它保留这些所有的抽象方法，它implements接口，并让那些实现了接口的子类继承它。自己内部出了接口的全部抽象方法外，还可以新的具体方法{方法内只抛出异常}。子类根据需求增加新功能，需要新功能的，就重写那些方法，不需要的就别写。



#### Java Core 知识补充：**接口**

> Java Core 知识补充：**接口**
>
> 接口是抽象类的极致。只有抽象方法，没有实际方法。可以被多实现。
>
> 接口不是类，它是对希望符合这一接口的类的一组需求。Arrays类的sory()方法承诺可以对对象数组进行排休，但前提是该对象的类要实现了Comparable接口。（接口里定义的需求：int compareTo (Object o); ）
>
> 接口的方法都是自动public。接口的属性都是自动public static final，即都是常量（有final必须直接赋值）。
>
> 接口没有实例。**1.8版本之后，接口可以提供一些简单的具体方法，但是不能引用实例字段，只能引用静态属性字段。**
>
> 接口不是类，所以没有实例。但是可以有接口变量：Compareble x; 接口变量必须引用一个实现了该接口的类的对象。**(多态)!**
>
> 可以包含多个抽象方法（需求）。
>
> 一个类要实现一个接口：
>
> 1. implements    2. 实现接口定义的方法
>
> **instanceof  检查一个对象是否属于一个类，也可以检查一个对象的类是否实现了接口：**
>
> 1. **对象 instanceof 类      2. 对象 instanceof 接口**
>
> 接口也可以有继承：从通用性较高的接口，到专用性较高的接口
>
> 接口可以多实现：class Employee implements Cloneable, Comparable{...}  这意味着，你可以使用.clone()和.sort()方法了。
>
> 一个类可以继承一个类，多实现n个接口：
>
> ```java
> class Employee extends Person implements Cloneable, Comparable{
>   ...
> }
> ```
>
> 接口和抽象类：为什么要引入接口概念？ **类 implements 接口**  vs **类 extends 抽象类**
>
> * 因为extends只能继承一个类，而implements可以实现多接口
> * 接口提供了多继承的大多数好处，避免了多继承的复杂性和低效率



#### Java Core 知识补充：**抽象类**

> Java Core 知识补充：**抽象类**
>
> 原因：越上层的类约抽象，它对对象的信息提供就非常少。
>
> 目的：为了提高程序的清晰度，知道这个抽象类到底为一个对象提供哪些信息，我们使用抽象概念。即让一个类本身是abstract，里面除了包含自身的属性，就是本身不打算提供具体方法的(一个或多个)抽象方法。
>
> eg：一个Person类，被Employee类和Student类继承。它提供一些具体方法，也提供抽象方法。
>
> ```java
> abstract class Person{//不写: 本类 同包可访问 ---> 包外的类，想import这个包来使用这个类，是不可以的
>    private String name;
>    Person(String name){ this.name = name; } //构造方法 --> 构造方法一般要public 因为要所有类都可以用 前提是类是共有
>    String getName(){  return this.name;  }  //具体方法
>    public abstract String getDescription(); //抽象方法
> }
> class Student extends Person{
>     ①属性major; ②构造器Student{super(name);...} ③具体化方法getDescription(){...} ④方法study(){...} 
> }
> class Empolyee extends Person(
> 	①属性salary; ②构造器Employee{super(name);...} ③具体化方法getDescription(){...} ④方法riseSalary(){...} 
> )
> ```
>
> **建议尽量把通用字段和方法放在超类中（不论是不是抽象类，不论是不是抽象方法）** ---> 在子构造器中调用父构造器完成那些字段的初始化。再初始化自己的字段。
>
> 抽象方法充当占位角色，具体由子类实现。
>
> 抽象类不能实例化。可以有抽象类的变量，但只能引用具体化了的子类的对象。Person p = new Student();  **(多态)!**
>
> 不含抽象方法，也可以声明为抽象类。抽象类不能实例化。
>
> 问题：为什么不直接只在Student和Employee类中写getDescription()方法，还要在Person里放一个抽象方法？
>
> * 因为，这样p变量就可以调用getDescription()方法，并且根据不同的实际对象给出不同的返回结果。**(多态)!**
> * 如果Person里不写这个抽象方法，p就不能调用getDescription()方法。



#### Java Core 知识补充：**static和final**

> Java Core 知识补充：**static和final**
>
> **static 静态** —— 属于该类的，存在方法区的静态区的该类空间中。
>
> 1. private static int nextId;   **静态字段**：属于类，而不属于任何一个对象。可以通过类名调，也可通过对象调。（可以不断改值）
>
> 2. public static final PI = 3.14;  **静态常量**：public静态常量是可以的，因为它final了，不会被改。
> 3. Math.pow(x,a);  **静态方法**：不在对象上执行。
>    * 什么时候使用静态方法：1. 方法不需要访问对象状态。  2. 方法只访问类的静态字段。
>
> **final 最终的** —— 不被更改：In Java, the **`final` keyword** can be used while declaring an entity(实体). Using the final keyword means that **the value can’t be modified in the future**.
>
> 1. 静态常量：public static final PI = 3.14; 类就一个static字段，而且final不能改，所以叫静态常量。final static必须声明时赋值。
> 2. final属性：class FinalTest{ final int x = 1;}  
>    * 权限符默认不写，就是本包和本类。本类里直接用；本包要通过本类的对象用，可以访问，可以改。
>    * final属性：要么声明时赋值。要么在构造函数和代码块赋值。final static属性必须声明时赋值。
> 3. final变量：方法中，final int a; 一旦赋值，不能再改。
> 4. final形参：这个形参在方法中不能被改变。public static  void test(final int a){ a = 3; } //这就报Error了。（static可以不写）
> 5. final方法：此方法 不能被overriden重写。
> 6. final类：此类不 能被extends继承。



#### 高内聚，低耦合

> 高内聚，低耦合 High aggregation and low coupling
>
> 内聚：每个模块尽可能独立完成自己的功能，不依赖于模块外部的代码。
> 耦合：模块与模块之间接口的复杂程度，模块之间联系越复杂耦合度越高，牵一发而动全身。
> 目的：使得模块的“可重用性”、“移植性”大大增强
> 通常程序结构中各模块的内聚程度越高，模块间的耦合程度就越低
>
> **模块粒度：**
> 『函数』
> 高内聚：尽可能类的每个成员方法只完成一件事（最大限度的聚合）
> 低耦合：减少类内部，一个成员方法调用另一个成员方法
> 『类』
> 高内聚低耦合：减少类内部，对其他类的调用
> 『功能块』
> 高内聚低耦合：减少模块之间的交互复杂度（接口数量，参数数据）
>
> 横向：类与类之间、模块与模块之间
> 纵向：层次之间
> 尽可能，内容内聚，数据耦合



#### This 和 super

> 父类的属性和方法，子类在自己内部使用：super.name  或者 super.getName()  注意调用的是自己创建时，生成的对象空间里的只为自己服务的父亲对象。如果调用的是类静态常量，类静态方法，那就无所谓，都可以。类常量和类静态方法——可以被对象调用，也可以直接用类调用。
>
> 属性：父类的属性，子类也有，this.name 那就是子类的name。如果子类没有，那就找父类的public属性和protected属性。
>
> ```java
> 父class: public String name;
> 子class: 构造函数(String name){this.name = name;}  //子类可以直接调用父类属性
> ```
>
> 老师写法和我写法的区别：
>
> * 老师总是在 类的内部自我调用时，方法和属性前面都放this。说是这个对象调用了其他方法。可是实际上也可以直接调用方法，前面不放this。不知道区别是什么？
> * 以及，this最核心的用法不是用来解决形参和属性的重名问题吗？
>
> super可以用于super构造器，和super.属性  super.方法()。反正super指代父对象（或者说父的那部分属性和功能）。
>
> super的使用形式：
>
> * super(String name, int age); 调用父的构造函数
> * super.name  父的属性
> * super.getName()  父的方法



属性和方法的访问权限问题

> 类：
>
> 属性：只能写声明，或声明+赋值。不能写赋值语句。
>
> * 属性可以在方法内写赋值语句。
>
> * 属性可以直接被本类所有方法直接使用。（需要区别对象属性和形参名时，用this，需要使用父类属性和父类方法，用super）
> * 如果一个属性定义在父类里（父类name），子类（没有name）直接用也没问题。
>   * { 方法体内：return name; }  或者 { 方法体内：return super.name; } ---> 二者效果一样。
>
> 方法：
>
> * this和super在方法内的用法。this指代调用方法时的对象。super指调用方法时的对象的父部分。
>
> * 还是那个要不要注明this的问题 ------> 尚未解决。





### 八、策略模式+内部类

调用一个方法，名字一样，传入参数不同

1. 利用方法重载 —— 静态加载
2. 利用多态 —— 动态加载（Person p = new Teacher(); Bank.oprating(p); )

#### 3. 策略模式 Strategy —— 行为型模型

执行流程是固定的，执行结果因提供了不同的策略而不同。

```java
class Bank{
   public 办业务 ( 人 ){   //人是抽象类或接口（不能产生实例）----> 传入的是子类对象
       欢迎用户;
       叫号;
       办业务;
       欢迎下次光临;
   }
}
```

### 九、内部类

目的：为了封装。

java中，一个类定义在另一个类内部。

内部类可以定义在，类的内部（和类成员同一个层次）。

也可以定义在方法/块的内部（和方法的局部变量一个层次）。

1. **成员内部类** —— 即 类 的内部

   * 可以像普通方法一样，使用权限修饰符和特征修饰符：public protected 不写 private static final abstract。外部类只有public和不写。

   * 好处：①省了一个源文件  ②该内部类可以访问所有外部类的成员(包括private元素) —— 直接写直接用，不能用this或super

   * 创建内部类对象：`Demo.InnerDemo ind = new Demo().new InnerDemo();`  

     * 在外部类内 要创建内部类对象  或  在主方法要创建内部类对象

     ```java
     Demo d = new Demo(); //先创建外部类对象
     Demo.InnerDemo ind = d.new InnerDemo(); //外部类对象 创建 内部类对象
     //或者
     import Demo.InnerDemo;
     InnerDemo ind = d.new InnerDemo();
     ```

   * 使用内部类方法：

     ```java
     ind.innerMethod();
     ```

   * 如果内部类和外部类有重名属性：name 是自己的。Demo.this.name是外部类的对象的。
   * 内部类编译后产生一个文件：Demo$InnerDemo.class

2. **局部内部类** —— 即 方法/构造函数/块 的内部（用的不多）

   * 局部内部类像局部变量一样，它只是个局部变量。所以不能用public protected private(修饰类成员的)及static。
   * 只能用abstract和final修饰
   * 局部内部类编译后：Demo$1innerDemo.class (重名的内部类，数字变成2)
   * 局部内部类的变量，必须用final修饰。用外部的成员属性都随便使用。

3. **匿名内部类** 

   * 成员匿名内部类

   * 局部匿名内部类

   * 通常接口或抽象类的具体子类写：

     ```java
     public interface Test{
       public void test();
     }
     Test t = new Test(){
       public void test(){...}//实现了接口的子类   不起名字，直接把类体写在这
     }
     ```

   * Test t = new Test(){ public ...}  这个结构写在类的属性里，就是成员匿名类；写在方法里，就是局部匿名类。
   * 开发中为了省略一个类文件。
   * 只有类体，没有类名，没有任何修饰符，也没构造方法。
   * 用于：Swing做按钮监听——按钮绑定一个事件监听器

4. **静态内部类** —— 在 类 的内部，就是成员内部类（静态内部类）

   * 不需要外部类对象，直接用外部类名＋内部类名即可创建（需要import外部类）

     `Demo.InnerClass inner = new Demo.InnerClass();`

   * 静态元素不能访问非静态元素（自己类和外部类的都不行）
   * private protected public 不写：都可以

### 十、枚举类

> java数据类型：
>
> 基本类型：8个
>
> 引用类型：数组[ ]  String  类class  抽象类abstract class   接口interface   枚举enum  注解@interface

没有他也行，只是有些时候，因为它的存在会更方便。

**枚举类：一个类的对象是有限且固定的。**

没有枚举类之前，我们怎么达到这样的效果？

1. 私有化构造器，这样别人就不可以构造更多本类对象。
2. 把对象建立在属性里：

```java
class Day{
   //首先私有化构造器
   private Day(){}
   //其次，类似于单例模式，把对象构建在属性里。
   //①这个属性对象要可以被调用，所以要public
   //②不能通过构造新的类对象来访问这个属性，只能通过类名来访问这个属性，所以要static
   //③它不可以被随便改值，所以要final
   public static final Day Monday = new Day();
   public static final Day Tuesday = new Day();
   public static final Day Wednesday = new Day();
   public static final Day Thursday = new Day();
   public static final Day Friday = new Day();
   public static final Day Saturday = new Day();
   public static final Day Sunday = new Day();
   //一般属性随便设计即可
}
//使用这些对象：
   Day day = Day.Monday;
```

枚举类：

```java
public enum Day{Monday,Tuesday,Wednesday,Thursday,Friday,Saturday,Sunday}
//使用：
   Day day = Day.Monday;
```

接口没有父类。

> 所以接口是干嘛用的？
>
> ① Java core的说法是，你要想使用一些方法，必须实现某个接口。比如你想用.sort()方法，必须实现CompareTo接口。
>
> ② 接口定义了一系列规则(需求)，实现类必须实现里面的接口。于是可以用接口对象 实现多态。

但是枚举类是一个正常的类，它默认继承了Object类，还默认继承了Enum类 —— 所以枚举类不能再继承其他类。

Enum类：抽象类