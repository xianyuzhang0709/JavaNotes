# Chapter 4,5 review tips

子类从父类延伸而来：extends

```java
public class Manager extends Empolyee{ ... }
```

Overriding 重写父类的 methods：

```java
//1.在子类的方法中，调用父类的方法：
super.getSalary();

//2.在子类构造器中调用父类构造器：
public manager(String name, double salary, int year, int month, int day){
  super(name,salary,year,month,day); //父类构造器
  bonus = 0;
}
```

```java
//3.在一个类中，一个构造器，调用自己的另一个构造器
public Employee(double s){
  this("Employee #" + nextId, s);//这个方法只输入了salary，但是name用了"Employee #" + nextId。调用另一个构造器，完成自己的构造。
}
public Employee(String n, double s){
  name = n;
  salary = s;
}
```

### 4. 在类中调用方法:

```java
//书上例子：
import java.util.Objects;
public class Employee{
  public String toString(){
    return getClass().getName()+"[name ="+name .....; //直接使用Objects.getClass()  
  }
}
```

本类的static方法：methodName();

本类的非static方法：本类对象.methodName();

