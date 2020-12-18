# Exceptions, Assertions, and Logging

> 程序会遇到错误。
>
> 要么在本方法中抛出异常，让后面的程序捕获，或者后面的程序也继续传递异常，直到被异常被捕获处理。
>
> 异常被捕获处理后，方法就不会再抛出异常。

### 处理错误：

由于出现错误而导致某些操作没有完成：

* 返回一种安全状态，并能够让用户执行其他命令；
* 允许用户保存所有工作的结果，并以妥善方式终止程序。

Runtime Exception是程序编写的有问题。应主动避免。unchecked exceptions.

**IOException**是I/O类型的错误导致的异常。我们主要针对这种异常进行处理。**checked exceptions.**

### 声明异常：

如果你写的方法可能会导致一个异常，你必须告诉调用这个方法的程序员，这个方法可能抛出一个异常。因为任何一个抛出异常的方法都可能是死亡陷阱。如果没有处理器捕获这个异常，执行的线程就会终止。

在方法的首部指出这个方法可能导致异常：

```java
class MyAnimation{
  public Image loadImage(String s) throws FileNotFoundException, EOFException{
    ...
  }
}
```

* 一个方法必须抛出所有可能抛出的checked exceptions。

### 抛出异常：

```java
throw new EOFException();
//或
var e = new EOFException();
throw e;
```

```java
String readData(Scanner in) throws EOFException{
  while(...){
    if(!in.hasNext())//EOF encountered
    {if (n<len)
      String gripe = "Content-length: "+len+",Received: "+n;
    	throw new EOFException(gripe);
    }
    ...
  }
  return s;
}
```

如果你的类可能抛出的异常类型已有：

1. 找到合适的异常类
2. 创建这个类的一个对象
3. 抛出对象

一旦方法抛出异常，这个方法就不会返回到调用者。所以不需要建立默认返回值或错误码。

### 创建异常类：

自定义的异常类应该包含两个构造器：

1. 默认的构造器
2. 一个包含详细描述信息的构造器（使用超类Throwable的toString方法返回一个字符串，其中包含详细信息）

```java
class FileFormatException extends IOException{ //自定义的异常类
  public FileFormatException(){}
  public FileFOrmatException(String gripe){
    super(gripe);
  }
}
```

# Catching Exceptions捕获异常

### 捕获异常：

```java
try{
  ...//操作语句，这里可能抛出异常
}
catch(ExceptionType1 e1)
{
  ...//在这里处理异常
}
catch(ExceptionType2 e2)
{
  ...//在这里处理异常
}
```

try语句块中的任何代码，如果抛出catch语句中的一个异常类，那么：

1. 程序将跳过try语句的其他部分
2. 执行catch语句的处理代码

如果try没有抛出任何异常，则不执行catch语句

如果try抛出异常，catch却没有声明这种异常，这个**方法会立即退出**。

> **编译器会严格处理throw语句**，如果你在你的方法中调用了一个会抛出异常的方法（比如`public void read(String filename) throws IOException{...}`)，就必须处理这个异常，或者继续传递这个异常。
>
> 怎么做呢？捕获你能处理的异常，传递你不能处理的异常。

另外，

> 如果你编写了一个override超类方法的方法，而这个超类方法没有声明任何异常，那么你的方法也不能声明任何异常，你必须捕获你的异常（检查型异常）。
>
> 即，不允许子类的throws说明符中出现超类方法没有列出来的异常类型。

```java
e1.getMessage()  //获得详细的错误信息（如果有的话
e1.getClass()getName()  //获得错误类型名字
```

### 捕获异常并再次抛出：

在catch字句中抛出异常：（通常，用于**改变异常类型**）

eg：你在开发一个子系统供别的程序员使用，可以使用一个指示子系统故障的异常类型。（我的理解是，系统抛出异常，然后换成子系统异常）。

```java
try{
  access the database
}catch(SQLException e){
  var e = new ServeletException("database error");
  e.initCause(original);//把原始异常设置为新异常的原因
  throw e;//捕获异常再抛出
}
```

捕获这个异常时，可以使用下面的语句获得原始异常：

```java
Throwable original = caughtException.getCause();
```

### 代码抛出一个异常时，会停止执行这个方法的剩余代码，并退出这个方法。如果这个方法获得了一些本地资源，而这些资源必须处理。finally字句：

**不论是否有异常被捕获，finally子句都会被执行。**

```java
var in  = new FileInputStream(...);
try{//1
  code that might throw exceptions
//2}
catch(IOException e)
{//3
  show error message;
//4}
finally{//5
  in.close();
}//6
```

1. 如果代码没有抛出异常：`1256`
2. 代码抛出异常，catch捕获：try语句执行到异常抛出位置，转去匹配的catch语句，最后执行finally子句
   1. catch没有异常：`13456`（正常处理完异常，继续执行）
   2. catch抛出异常：异常抛给方法调用者，`135`，（finally还是执行了，并且不会再往下执行）
3. 代码抛出异常，没有catch捕获：try语句执行到异常抛出，执行finally，异常抛给方法调用者。`15`。

##### 改进版：

```java
InputStream in = ...;
try{
  try{
    //code that might throw exceptions
  }finally{
    in.close()
  }
}catch(IOException e){
  //show error message
}
```

内圈try-finally确保关闭输入流。外圈try-catch确保报告错误信息。

finally子句主要用于清理资源，不要把控制流的语句放在finally子句。

> From newCoder:
>
> ```java
> public class Test
> {
>     public static int aMethod(int i)throws Exception//这个方法声明了会有异常，但不一定必然抛出异常
>     {
>         try{
>             return i / 10;
>         }
>         catch (Exception ex)
>         {
>             throw new Exception("exception in a Method");
>         } finally{
>             System.out.printf("finally");
>         }
>     }
>     public static void main(String [] args)
>     {
>         try
>         {
>             aMethod(0);
>         }
>         catch (Exception ex)
>         {
>             System.out.printf("exception in main");
>         }
>         System.out.printf("finished");
>     }
> }
> ```
>
> 1、finally块一定会执行，无论是否try…catch。
>
> 2、finally前有return，会先执行return语句，并保存下来，再执行finally块，最后return。
>
> 3、finally前有return、finally块中也有return，先执行前面的return，保存下来，再执行finally的return，覆盖之前的结果，并返回。
>
> 本题最终结果：finally，finished。

