# Char & Unicode & String

![](/Users/zhangxianyu/JavaNotes/imgs/c401_char1.png)

![](/Users/zhangxianyu/JavaNotes/imgs/c401_char2.png)

**range**: `['\u0000', '\uffff']`是Unicode representation。`[0,65535]`是Integer representation。

A char 始终代表一个字符。它与binary之间，通过Unicode encoding scheme互相转化。

characters用单引号包括。

A char占2 bits内存。

![](/Users/zhangxianyu/JavaNotes/imgs/c401_char3.png)

你可以用`'A'`, `'\u0041'`, `65`来在Java中表示character 'A'。

* 一种是char字符本身；
* 一种是Unicode presentation；
* 一种是integer presentation。
* 它们在Java中，（如果你指定它是char type）都指向char字符'A'。

![](/Users/zhangxianyu/JavaNotes/imgs/c401_char4.png)

用三种方式表示，都指向char 'A'。

如果你要输出char对应的数值，将variable类型换成int即可：

![](/Users/zhangxianyu/JavaNotes/imgs/c401_char5.png)