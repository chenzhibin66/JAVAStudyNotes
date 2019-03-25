# JAVA面试208道

#### 1.JDK 和 JRE 有什么区别？ 

jdk是java的开发包，其中包括jre;jre仅仅是java的运行时环境；而JDK包括了同版本的JRE，此外还包括有编译器和其它工具  

#### 2.== 和 equals 的区别是什么？ 

“==”比较两个变量本身的值，即两个对象在内存中的首地址。

“equals()”比较字符串中所包含的内容是否相同。

#### 3.两个对象的 hashCode()相同，则 equals()也一定为 true，对吗？ 

equals相等，则hashcode一定相等，反之则不然。 如果重写equals后，如果不重写hashcode，则hashcode就是继承自Object的，返回内存编码，这时候可能出现equals相等，而hashcode不等，你的对象使用集合时，就会等不到正确的结果 

#### 4.final 在 Java 中有什么作用？

- final可以修饰类，这样的类不能被继承。 
-  final可以修饰方法，这样的方法不能被重写。  
-  final可以修饰变量，这样的变量的值不能被修改，是常量。 

####  5.Java 中的 Math.round(-1.5) 等于多少？ 

-1

#### 6.String 属于基础的数据类型吗？ 

String不是基本数据类型，而是一个类（class），是C++、java等编程语言中的字符串。 

而java的8大基本数据类型分别是：

- 整数类 byte, short, int, long

- 浮点类 double, float。

- 逻辑类 boolean
- 文本类 char

#### 7.Java 中操作字符串都有哪些类？它们之间有什么区别？ 

String、StringBuffer、StringBuilder

区别：String是不可变的对象，对每次对String类型的改变时都会生成一个新的对象，StringBuffer和StringBuilder是可以改变对象的。

对于操作效率：StringBuilder > StringBuffer > String

对于线程安全：StringBuffer 是线程安全，可用于多线程；StringBuilder 是非线程安全，用于单线程

不频繁的字符串操作使用 String。反之，StringBuffer 和 StringBuilder 都优于String

#### 8.String str="i"与 String str=new String(“i”)一样吗？ 

不一样，因为他们不是同一个对象。 