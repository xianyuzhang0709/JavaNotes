类之间的 关系：

* A    is-a   B   （泛化）继承  实现 

* A  has-a B   （包含） 组合  聚合   关联

* A  use-a B   （依赖） 依赖（need a）

### 一、继承 extends: is-a

1. 子类对象可以调用父类的（public和protected）的属性和方法。

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

   * 存在方法重载：有三个带不同参数的wait()方法

6. **notify()** :  线程唤醒

7. **notifyAll()** :  唤醒所有

8. **finalize()** :  protected方法，在对象被GC回收时，默认调用执行的方法。

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



