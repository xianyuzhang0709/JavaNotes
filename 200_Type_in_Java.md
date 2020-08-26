# Type in java - notes from Neso Academy

1. **Integers**: Numbers without a decimal part

   * `1, 2, 100, -4, -9, 0`

   **Real Numbers / Floting point Numbers**: numbers with a decimal part

   *  `1.5, 2.25, -4.7, -9.9, 1.0, 0.0`

   An interger can be a real number

   * `1.0, 2.0, 100.0, -4.0, -9.0, 0.0`

2. **Characters**: all characters on the keyboard - And More

   * `'a', '5', '-', '*', '?', '$', ';', ','`  surrounded with **single quotes**

3. **Strings**: group of characters - Text

   * `"a", "abc123", "()", "523", "hello", ""`

4. **Booleans**: the value represents `True` & `False`
   
* used to create conditions
   
5. **User defiend types**: create a custom type using Classes & Objects.

## 1. Integers

![](imgs/c402_int1.png)

#### byte, short, long

![](imgs/c402_byte1.png)

![](imgs/c402_short1.png)

![](imgs/c402_long1.png)

L3需要在数字后面加个L，来向compiler表示它是long类型。

而L2在integer范围内，所以即便不加L，compiler也不会出错，因为它会按照默认的int来编译。

## 2. conversion

![](imgs/c402_conversion.png)

![](imgs/c402_conversion2.png)

![](imgs/c402_conversion3.png)

* **it should be `long l1 = 999L;`**

![](imgs/c402_conversion4.png)

Besides, the value of the numbers cannot be changed. We only can change the reference of the varibale.

将integer变量相互加减操作后，variable对应的值不会变，Java只是输出了加减后的值，却不改变原值。

## 3. Bits and memory

![](imgs/c403_bits_&_memory1.png)

* **Our memory is divided in to bytes.**

![](imgs/c403_bits_&_memory3.png)

* check the range of a type:

![](imgs/c403_bits_&_memory4.png)

## 4. float and double

![](imgs/c404_float2.png)

![](imgs/c404_float1.png)

所有的floating number in java are considered **double**. 

当你声明了一个float而实际上给了一个默认的浮点数值：它会报错。应该是`float f1 = 4.5F;`

![](imgs/c404_float3.png)

当你写`double d1 = 10.6F;`系统会自动把float转成double。so不会报错。

当你写`float f1 = 4;` 不会报错，Java会把int直接转化成float 4.0。double 同理。

## 5. char & unicode & string

## 6. Boolean type

* Declare a boolean variable: `boolean b;`
* possible values: `true or false`
* initialize: `boolean b = true;` `boolean c = 2 < 3;//true`

The size of a boolean variable is not precisely defined, it depends on JVM.

## 7. string

**String class**: String is a class that contains some static methods.

**String objects**: Variables of type string, also have some methods.

![](imgs/c405_string1.png)

![](imgs/c405_string2.png)

* 观察Java的type declearition 方式：

  ```java
  byte b = -1;
  short s = 20;
  int i = 100;
  long l = -201;
  boolean bool = true;
  char c = 'a';
  
  String s = "hello";
  ```

  此处说明，String是类的对象，不是primitive type，所以是String。

##### **7.1 Calling methods of String:**

1. `strObj.toUpperCase()`

```java
String text = "This is some text";
System.out.println(text.toUpperCase());
```

![](imgs/c405_string3.png)

​	NOTE: the original String is not modified.

2. `strObj.length()` ""空串长度为0；space占一个长度。

3. `strObj.isEmpty()`是空串； `strObj.isBlank()`空串或只有空格。

4. `strObj.charAt()` 输出字符串的第( )个字符。

5. `strOj.indexOf(int character)`字符第一次出现的index；   `strOj.lastindexOf()`字符最后一次出现的index。

   * `ch` - a character (Unicode code point).

   ```java
   String s = "abcd";
   s.indexOf('a'); //在这填字符'a'和"a"，以及数字97，都是有效的
   ```

##### 7.2 concatenating string using "+"

When `+` is uesed with Strings it acts as a **concatenating operator**;

When `+` operator is used **only with numbers** it acts as an **addition operator**.

![](imgs/c405_string4.png)

如果给把`5+3`变成`(5+3)`，那么输出结果会是`...is 8`

##### 7.3 另一个concatenating方法是：`.concat()`。

```java
String a = "neso".concat(" academy").concat("5");
```

### 8. primitive types vs reference types

![](imgs/c406_primitive0.png)

* we have a box called i, inside it we have the value 15. Each box has an address.

![](imgs/c406_primitive1.png)

```java
int i1 = 5;
int i2 = i1;   //i1 and i2 are different, they contains distinct values.

String s1 = "hello";
String s2 = s1;  //s1 and s2 are different, but they reference the same value.
```

![](imgs/c406_primitive2.png)

### 9. Instantiating an object

![](imgs/c407_instantiate1.png)

![](imgs/c407_instantiate2.png)

### 10. Strings are immutable 

![](imgs/c408_immutable1.png)

Content 内容。Constant常数。

![](imgs/c408_immutable2.png)

![](imgs/c408_immutable3.png)

### 11. Literals in java

**Literals** are the **constant values** that appear directly in a program.

```java
//String literals : "hello"和"this is some text"
String s = "hello";
System.out.println("this is some text");

//Character literals : 'a'和'c'
char c = 'a';
System.out.println('c');

//Integer literals : 123和156
int i = 123;
System.out.println(456);

//Floating point : 15.6和9.6F
System.out.println(15.6);
System.out.println(9.6F);

//Boolean literals : true和false
boolean b1 = true;
boolean b2 = false;
```

