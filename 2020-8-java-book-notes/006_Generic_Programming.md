# 泛型

泛型的目的是，代码对不同类型的对象都可以重用。

* 允许泛型代码和遗留代码之间互相操作。

> 泛型中常用字母：E表示List，T表示任意类型，K和V表示Key和Value。

### 1. 泛型类

```java
public class Pair<T>{
  ...
}
```

### 2. 泛型方法

```java
public static <T extends Comparable> boolean contains(Collection<T> ct){
  ...
}
```

### 3. 类型变量限定

限定类型(Bounding Type)：使用**extends**来标识泛型受限于什么类型。extends后面可以跟无数个接口和一个类。如果有类，必须写在第一个。

### 4. 泛型擦除

主要发生在泛型方法调用、泛型类的属性访问，和泛型方法中。

泛型擦除触发在表达式中：当然是方法调用和属性访问时。擦除的方法是不同的。

##### 4.1 为什么泛型擦除？

因为，java虚拟机中没有泛型类型对象（objects of generic types），所有对象都是普通类。虚拟机中， 如果你定义了一个泛型类型，会自动为你生成了一个原始类型（原始类），这原始类型，就是就是擦除掉反省变量以后的类。

* 原始类的生成规则是：类名去掉泛型参数。所有属性和方法体中，都用限定类型（唯一父类/接口）来代替。如果没有限定类型，就用Object代替。
* 如果限定类型是Comparable & Serializable，那么类/方法中所有的泛型所在的地方，都会被换成Comparable

##### 4.2 泛型擦除时，如何解决泛型表达式中的泛型（使之保持泛型效果）？

其次，调用泛型方法时：因为类型擦除，方法返回的是Object类型的对象，而你要接收的是自定义的类型`<String>`，compiler会自动插入强制类型转换，转为你想要的类型。

```java
Pair<Employee> buddies = ...;
Employee buddy = buddies.getFirst();
```

在.getFirst()方法执行时（此方法是泛型方法——因为返回类型是泛型），自定擦除的结果（擦除是虚拟机在接收你定义的泛型类和方法时的本质操作）会给你返回一个Object类型的对象。在这里，会插入一个强制类型转换。

同理，在访问泛型类的泛型属性时，也会为你自动插入强制类型转换。

##### 4.3 泛型擦除时，如何解决泛型方法中的泛型（使之保持泛型效果）？

泛型方法中，泛型出现的地方，也会被擦除和替换。（方法名中擦除，方法体中替换）

那么这里会出现一个问题：如果我们定义了一个类DateInterval，继承自另一个泛型类Pair`<LocalDate>`。

```java
class DateInterval extends Pair<LocalDate>{
  public void setSecond(LocalDate second){
    super.setSecond(second);
  }
}
```

虚拟机擦除以后：

```java
class DateInterval extends Pair{
  public void setSecond(LocalDate second){
    super.setScond(second);
  }
}
```

问题是，这个DateInterval类有自定义的.setSecond(LocalDate second)方法，也有继承自Pair的.setSecond(Object second)方法

这是两个不同的方法，因为参数不同。（所以这也不是重写）

当执行：

```java
Pair<LocalDate> pair = new DateInterval(...);
pair.setSecond(aDate); 
```

此时pair调用的是Pair类的.setSecond(Object o)的方法。

但是我们想要的是，多态的效果，pair应该调用执行真实对象的方法。

虚拟机会做一个工作：产生一个桥方法。

```java
在DateInterval类中：
  public void setSecond(Object o){
    setSecond((LocalDate) o);  //传入的参数进行了强制类型转化
	}
```

这样，DateInterval类就重写了.setSecond()方法。可以实现多态效果。消除了泛型擦除所带来的问题。

另外，如果DateInterval类中也有.getSecond()方法，这个方法和Pair的.getSecond()方法一样都没有参数。只是这两个方法的返回类型不同。一个是LocalDate，一个是Object。

但是这个问题，虚拟机可以正确处理，因为虚拟机会根据参数类型和返回类型来找到指定的方法。

##### 4.4 总结：java中泛型的转换

* 虚拟机中没有泛型，只有普通的类和方法
* 所有类型参数都会被替换为它的限定类型
* 会合成桥方法来保持多态（里面有强制类型转换）
* 为了保持类型安全性，必要时会插入强子类型转换

### 4. 泛型类的限制和局限性

1. 不能用基本类型实例化类型参数：只有`Pair<Double>` ，没有`Pair<double>`
2. 运行时类型查询只适用于原始类型
3. 不能创建参数化类型的数组：Pair`<String`[] table = new Pair`<String>`[10]; //不可以！
   * 因为数组会记住元素类型，如果试图存入其他类型，会抛出异常ArrayStroreException。
   * 泛型的类型擦除会使这种机制无效。
   * 声明泛型数组变量合法，但是不能实例化。
   * 需要收集参数化类型对象时，可以这样用：`ArrayList<Pair<String>>`





