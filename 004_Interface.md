# Interface 接口

##### 1. 如果你要使用Arrays类中的`.sort()`方法，你所用的类，就要实现Comparable接口。

```java
public interface Comparable{
  int compareTo(Object other);
}
```

* 接口可以定义常量。但没有实例字段。
* 接口中所有方法都是public，所以不用写public。
* 接口可以有简单的实现方法。

接口定义了方法，但没有实现。

##### 下面将Employee类实现接口Comparable。(泛型)

```java
class Employee extends Person implements Comparable<Employee>, Cloneable{
  public int compareTo(Employee other){
    return Double.compare(salary, other.salary);
  }
}
```

所以Employee的对象，可以**使用**`.sort()`方法。

例如：

```java
var a = new Employee[10];
//a赋值以后。。。
a.sort();
```

##### 2. callback回调

java.swing包中的Timer类，根据时间间隔，定期调用一个函数。你可以向定时器传入某个类的对象，然后定时器调用这个方法。

这个方法所属的类，必须实现了java.awt.event包的ActionListener接口。

```java
public interface ActionListener{
  void actionPerformed(ActionEvent event);
}
```

我们写一个类，来实现这个接口：

```java
class TimePrinter implements ActionListener{
  public void actionPerformed(ActionEvent event){
    System.out.println("At the tone,the time is "+ Instant.ofEpochMilli(event.getWhen()));
		Toolkit.getDefaultToolkit().beep();
  }
}
```

使用这个方法：

```java
Timer t = new Timer(1000, new TimePrinter());//注意，TimePrinter()是一个默认的空构造器。类中没有写，则系统自动生成一个。
t.start();  //开始执行
JOptionPane.showMessageDialog(null, "Quit program?");//询问是否结束
System.exit(0);//用户点击ok后结束
```

使用**Timer方法**要调用这个**TimePrinter类的实例/对象**。

##### 3. 比较器接口 Comparator Interface

.sort()对字符串数组排序时，是根据字典顺序排序。

我们想设计一个根据字符串长度排序的方法。

**Array.sort()还有第二个版本**，由**一个数组**和**一个比较器**作为参数。这个比较器，是实现了Comparator接口的类的实例。

```java
public interface Comparator<T>{
  int compare(T first, T second);
}
class LengthComparator implements Comparator<String>{
  public int compare(String first,String second){  //注意这里要写public
    return first.length()-second.length();
  }
}
```

当我们要进行比较时：

```java
var comp = new LengthComparator();
if(comp.compare(word[i],word[j])>0)...
```

这个是**在比较器上进行比较**，而不是在对象上进行比较。（对象上比较：`word[i].compareTo(word[j])`  ）

Array.sort()**对数组排序**时：一个数组+一个构造器

```java
String[] friends = {"harry","jane","pual"};
Array.sort(friend, new LengthComparator());
```

