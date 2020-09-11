# Java classes

OOP

Classes/Objects

Class Attributes

Class methods

# Encapsulation

The meaning of **Encapsulation**, is to make sure that "sensitive" data is hidden from users. To achieve this, you must:

- declare class variables/attributes as `private`
- provide public **get** and **set** methods to access and update the value of a `private` variable

# Java Packages & API

## Polymorphism

is a concept by which we can perform a *single action in different ways*.

Polymorphism is derived from 2 Greek words: poly and morphs. The word "poly" means many and "morphs" means forms. So polymorphism means many forms.

> There are two types of polymorphism in Java: **compile-time polymorphism** and **runtime polymorphism**. We can perform polymorphism in java by method overloading and method overriding.
>
> If you overload a static method in Java, it is the example of compile time polymorphism. Here, **we will focus on runtime polymorphism** in java.

**Runtime polymorphism** or **Dynamic Method Dispatch** is a process in which a call to an overridden method is resolved at runtime rather than compile-time.

[另一部分笔记参见《000_Java_Core》的#Polymorphism部分](../blob/master/000_Java_Core.md)

# Overload vs overriade

Overload是构造器重构。

Override是方法重写。

![](imgs/OverridingVsOverloading.png)

*—— From [GeeksforGeeks/ploymorphism](https://www.geeksforgeeks.org/polymorphism-in-java/)*

