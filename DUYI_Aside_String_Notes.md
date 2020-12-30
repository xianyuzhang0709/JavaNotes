# String

String类 represents character strings. 

All string literals in java program, such as "abc", are implemented as instances of this class. //Java中所有的字符串字面量，都实现为这个类的实例。

Strings are constant.  //String是常量。

Their values cannot be changed after they are created. String butters support mutable strings.

Because String objects are immutable thsy can be shared. //因为Sting对象的不可变性，所以他们可以共享。

##### String的用法：

```java
String str = "abc";
//is equivalent to:
char data[] = {'a', 'b', 'c'};  
String str = new String(data);
```

```java
System.out.println("abc");
String cde = "cde";
System.out.println("abc" + cde);
String c = "abc".substring(2,3);  //注意可以这样使用
String d = cde.substring(1, 2);
```

String构造函数：

1. 无参--> ""空串
2. 有参：byte[] bytes, [int offset, int length,] [Charset charset/String charsetName]
   * 由于byte不像char，什么字符都能存下，所以需要增加charset或charsetName来判断存的数值需要多少位。
3. 有参：char[] value, [int offset, int count]
4. 有参：int[] codePoints, int offset, int count
5. 有参：String original
6. 有参：StringBuffer/StringBuilder buffer/builder

String类的方法包括：

1. for examining individual characters of the sequence
   1. (**char**) <---  s**.charAt(int index)**  //Returns the `char value` at the specified index.
   2. (**int**) <---  s**.codePointAt(int index)**  //Returns the character (`Unicode code point`) at the specified index.
   3. (**int**) <---  s**.codePointBefore (int index)**  //Returns the character (`Unicode code point`) before the specified index.
   4. (**int**) <---  s**.codePointCount (int beginIndex, int endIndex)** //the number of Unicode code points in the specified text range of this `String`

2. for comparing strings

   1. (**int**) <--- s**.compareTo (String anotherString)**  //Compares two strings lexicographically.  (得到的值是：最近的在相同位置上的不同字符之间char值的相减值：`this.charAt(k) - another.charAt(k)`)  positive表示this大，在后；negative表示this小，在前。

      * 字典次序：如果两个strings不同，可能是某些index位置上的字符不同，或是长度不同。
      * 如果字符不同，找到最小的不同字符的index位置：`this.charAt(k) - anotherString.charAt(k)`  
      * 如果没有字符不同，而是长度不同：return `this.length() - anther.length()`

   2. (**int**) <--- s**.compareToIgnoreCase (String aString)**  //忽略大小写的compare

      * case differences was eliminated by calling `Character.toLowerCase(Character.toUpperCase(character))` on each character.

   3. (**boolean**) <--- s**.contentEquals (CharSequence cs / String Buffer sb)** //Compares this string to the specified `CharSequence /StringBuffer`.

   4. (**boolean**) <--- s**.equals (Object anObject)**  //The result is `true` if and only if the argument is not `null` and is a `String` object that represents the same sequence of characters as this object.

   5. (**boolean**) <--- s**.equalsIgnoreCase (Object anObject)** 

      > Two characters `c1` and `c2` are considered the same ignoring case if at least one of the following is true:
      >
      > - The two characters are the same (as compared by the `==` operator)
      > - Applying the method [`Character.toUpperCase(char)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#toUpperCase-char-) to each character produces the same result
      > - Applying the method [`Character.toLowerCase(char)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#toLowerCase-char-) to each character produces the same result

3. for searching strings

   1. (**boolean**) <--- s**.contains (CharSequence cs)**  //如果包含，则返回true
   2. (**boolean**) <--- s**.endsWith (String str)**
   3. (**boolean**) <--- s**.startWith (String str)**
   4. (**int**) <--- s**.indexOf(int ch, [int fromIndex])**  //返回ch所对应的字符在s中第一次出现的index值
   5. (**int**) <--- s**.indexOf(String str, [int fromIndex])**  //字符串str在s中第一次出现的index值
   6. lastindexOf同上

4. for extracting substrings

   1. (**CharSequence**) <--- s**.subSequence**(int beginIndex, int endIndex)
   2. (**String**) <--- s.**subString**(int beginIndex, [int endIndex])
   3. (**String**) <--- s**.trim**()  //前后空格删除，返回字符串

5. for concating strings

   1. (**String**) <--- s**.concat (String str)**  //Concatenates the specified string to the end of this string.
   2. (**byte[]**) <--- s**.getByte([Charset charset / String charsetName])** //Encodes this `String` into a sequence of bytes using the platform's default charset, storing the result into a new byte array.

6. for creating a copy of a string with all characters translated to uppercase or to lowercase. Case mapping is based on the Unicode Standard version specified by the [`Character`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html) class.

7. for sepecial manipulating:

   1. (**int**) <--- s**.hashCode**()  //运算方式为：`s[0]*31^(n-1) + s[1]*31^(n-2) + ... + s[n-1]`

   2. (**int**) <--- s**.length**()

   3. (**String**) <--- s**.toString**()  //This object (which is already a string!) is itself returned.

   4. (**String**) <--- s**.replace**(char oldChar, char newChar)

      (**String**) <--- s**.replace**(CharSequence target, CharSequence replacement)

      replaceAll(String regex, String replacement)

      replaceFirst(String regex, String replacement)

   4. (**String[]**) <--- s**.split(String regex, [int limit])**  //Splits this string around matches of the given [regular expression](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html#sum).
   5. (**void**) <--- s**.getChars** (int srcBegin, int srcEnd, **char[] dst**, int dstBegin)  //Copies characters from this string into the destination character array —— char[] dst.
   6. (**char[]**) <--- s**.toCharArray**()  //Converts this string to a new character array.

* Unless otherwise noted, passing a `null` argument to a constructor or method in this class will cause a [`NullPointerException`](https://docs.oracle.com/javase/8/docs/api/java/lang/NullPointerException.html) to be thrown.

注意String的不可变性。所有更改String的方法，都是返回新的字符串出来。



| Modifier and Type | Method                                           | Description                                                  |
| ----------------- | ------------------------------------------------ | ------------------------------------------------------------ |
| `char`            | **charAt**(int index)                            | Returns the `char` value at the specified index.             |
| `int`             | **codePointAt**(int index)                       | Returns the character (Unicode code point) at the specified index. |
| `int`             | **codePointBefore**(int index)                   | Returns the character (Unicode code point) before the specified index. |
| `int`             | **codePointCount**(int beginIndex, int endIndex) | Returns the number of Unicode code points in the specified text range of this `String`. |
| `int`             | **compareTo**(String anotherString)              | Compares two strings lexicographically.                      |
| `int`             | **compareToIgnoreCase**(String str)              | Compares two strings lexicographically, ignoring case differences. |
| `boolean`         | **contains**(CharSequence s)                     | Returns true if and only if this string contains the specified sequence of char values. |
| `boolean`         | **contentEquals**(CharSequence cs)               | Compares this string to the specified `CharSequence`.        |
|                   |                                                  |                                                              |
|                   |                                                  |                                                              |
|                   |                                                  |                                                              |
|                   |                                                  |                                                              |
|                   |                                                  |                                                              |
|                   |                                                  |                                                              |
|                   |                                                  |                                                              |
|                   |                                                  |                                                              |
|                   |                                                  |                                                              |
|                   |                                                  |                                                              |
|                   |                                                  |                                                              |
|                   |                                                  |                                                              |
|                   |                                                  |                                                              |
|                   |                                                  |                                                              |
|                   |                                                  |                                                              |
|                   |                                                  |                                                              |
|                   |                                                  |                                                              |
|                   |                                                  |                                                              |
|                   |                                                  |                                                              |
|                   |                                                  |                                                              |
|                   |                                                  |                                                              |

