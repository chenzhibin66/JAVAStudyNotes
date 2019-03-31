# JAVA基础

#### 1.JDK 和 JRE 有什么区别？ 

- JDK：Java Development Kit 的简称，java 开发工具包，提供了 java 的开发环境和运行环境。

- JRE：Java Runtime Environment 的简称，java 运行环境，为 java 的运行提供了所需环境。  

  具体来说 JDK 其实包含了 JRE，同时还包含了编译 java 源码的编译器 javac，还包含了很多 java 程序调试和分析的工具。简单来说：如果你需要运行 java 程序，只需安装 JRE 就可以了，如果你需要编写 java 程序，需要安装 JDK。 

#### 2.== 和 equals 的区别是什么？ 

== 对于基本类型来说是值比较，对于引用类型来说是比较的是引用；而 equals 默认情况下是引用比较，只是很多类重新了 equals 方法，比如 String、Integer 等把它变成了值比较，所以一般情况下 equals 比较的是值是否相等。 

#### 3.两个对象的 hashCode()相同，则 equals()也一定为 true，对吗？ 

equals相等，则hashcode一定相等，反之则不然。 如果重写equals后，如果不重写hashcode，则hashcode就是继承自Object的，返回内存编码，这时候可能出现equals相等，而hashcode不等，你的对象使用集合时，就会等不到正确的结果 

#### 4.final 在 Java 中有什么作用？

- final可以修饰类，这样的类不能被继承。 
-  final可以修饰方法，这样的方法不能被重写。  
-  final可以修饰变量，这样的变量的值不能被修改，是常量。 

####  5.Java 中的 Math.round(-1.5) 等于多少？ 

等于 -1，因为在数轴上取值时，中间值（0.5）向右取整，所以正 0.5 是往上取整，负 0.5 是直接舍弃。 

#### 6.String 属于基础的数据类型吗？ 

String 不属于基础类型，基础类型有 8 种：byte、boolean、char、short、int、float、long、double，而 String 属于对象。 

#### 7.Java 中操作字符串都有哪些类？它们之间有什么区别？ 

String、StringBuffer、StringBuilder

区别：String是不可变的对象，对每次对String类型的改变时都会生成一个新的对象，StringBuffer和StringBuilder是可以改变对象的。

对于操作效率：StringBuilder > StringBuffer > String

对于线程安全：StringBuffer 是线程安全，可用于多线程；StringBuilder 是非线程安全，用于单线程

不频繁的字符串操作使用 String。反之，StringBuffer 和 StringBuilder 都优于String

#### 8.String str="i"与 String str=new String(“i”)一样吗？ 

不一样，因为内存的分配方式不一样。String str="i"的方式，java 虚拟机会将其分配到常量池中；而 String str=new String("i") 则会被分到堆内存中。 

#### 9.如何将字符串反转？ 

```java
/**
 * 二分递归地将后面的字符和前面的字符连接起来
 *
 * @param s
 * @return
 */
public static String reverse1(String s) {
    int length = s.length();
    if (length <= 1) {
        return s;
    }
    String left = s.substring(0, length / 2);
    String right = s.substring(length / 2, length);
    return reverse1(right) + reverse1(left);
}

/**
 * 取得当前字符并和之前的字符append起来
 *
 * @param s
 * @return
 */
public static String reverse2(String s) {
    int length = s.length();
    String reverse = "";
    for (int i = 0; i < length; i++) {
        reverse = s.charAt(i) + reverse;
    }
    return reverse;
}

/**
 * 将字符从后往前的append起来
 *
 * @param s
 * @return
 */
public static String reverse3(String s) {
    char[] array = s.toCharArray();
    String reverse = "";
    for (int i = array.length - 1; i >= 0; i--) {
        reverse += array[i];
    }
    return reverse;
}

/**
 * 和StringBuffer()一样,都用java自实现的方法,使用位移来实现
 *
 * @param s
 * @return
 */
public static String reverse4(String s) {
    return new StringBuilder(s).reverse().toString();
}

/**
 * 和StringBuilder()一样,都用java自实现的方法,使用位移来实现
 *
 * @param s
 * @return
 */
public static String reverse5(String s) {
    return new StringBuffer(s).reverse().toString();
}

/**
 * 二分交换,将后面的字符和前面对应的那个字符交换
 *
 * @param s
 * @return
 */
public static String reverse6(String s) {
    char[] array = s.toCharArray();
    int end = s.length() - 1;
    int halfLength = end / 2;
    for (int i = 0; i < halfLength; i++) {
        char temp = array[i];
        array[i] = array[end - i];
        array[end - i] = temp;
    }
    return new String(array);
}

/**
 *
 * 基于栈先进后出的原理
 * @param s
 * @return
 */
public static String reverse7(String s) {
    char[] array = s.toCharArray();
    Stack<Character> stack = new Stack<>();
    for (int i = 0; i < array.length; i++) {
        stack.push(array[i]);
    }
    String reverse = "";
    for (int i = 0; i < array.length; i++) {
        reverse += stack.pop();
    }
    return reverse;
}
```

#### 10.String 类的常用方法都有那些？ 

1、求字符串长度 **public int length()**//返回该字符串的长度

```java
1 String str = new String("asdfzxc");
2 int strlength = str.length();//strlength = 7 
```

2、求字符串某一位置字符 **public char charAt(int index)**//返回字符串中指定位置的字符；注意字符串中第一个字符索引是0，最后一个是length()-1。 

```java
1 String str = new String("asdfzxc");
2 char ch = str.charAt(4);//ch = z
```

3、提取子串 用String类的substring方法可以提取字符串中的子串，该方法有两种常用参数: 1)**public String substring(int beginIndex)**//该方法从beginIndex位置起，从当前字符串中取出剩余的字符作为一个新的字符串返回。 2)**public String substring(int beginIndex, int endIndex)**//该方法从beginIndex位置起，从当前字符串中取出到endIndex-1位置的字符作为一个新的字符串返回。 

```java
1 String str1 = new String("asdfzxc");
2 String str2 = str1.substring(2);//str2 = "dfzxc"
3 String str3 = str1.substring(2,5);//str3 = "dfz"
```

4、字符串比较 1)**public int compareTo(String anotherString)**//该方法是对字符串内容按字典顺序进行大小比较，通过返回的整数值指明当前字符串与参数字符串的大小关系。若当前对象比参数大则返回正整数，反之返回负整数，相等返回0。 2)**public int compareToIgnore(String anotherString)**//与compareTo方法相似，但忽略大小写。 3)**public boolean equals(Object anotherObject)**//比较当前字符串和参数字符串，在两个字符串相等的时候返回true，否则返回false。 4)**public boolean equalsIgnoreCase(String anotherString)**//与equals方法相似，但忽略大小写。 

```java
1 String str1 = new String("abc");
2 String str2 = new String("ABC");
3 int a = str1.compareTo(str2);//a>0
4 int b = str1.compareToIgnoreCase(str2);//b=0
5 boolean c = str1.equals(str2);//c=false
6 boolean d = str1.equalsIgnoreCase(str2);//d=true
```

5、字符串连接 **public String concat(String str)**//将参数中的字符串str连接到当前字符串的后面，效果等价于"+"。 

```java
1 String str = "aa".concat("bb").concat("cc");
2 相当于String str = "aa"+"bb"+"cc";
```

6、字符串中单个字符查找 1)**public int indexOf(int ch/String str)**//用于查找当前字符串中字符或子串，返回字符或子串在当前字符串中从左边起首次出现的位置，若没有出现则返回-1。 2)**public int indexOf(int ch/String str, int fromIndex)**//该方法与第一种类似，区别在于该方法从fromIndex位置向后查找。 3)**public int lastIndexOf(int ch/String str)**//该方法与第一种类似，区别在于该方法从字符串的末尾位置向前查找。 4)**public int lastIndexOf(int ch/String str, int fromIndex)**//该方法与第二种方法类似，区别于该方法从fromIndex位置向前查找。 

```java
1 String str = "I am a good student";
2 int a = str.indexOf('a');//a = 2
3 int b = str.indexOf("good");//b = 7
4 int c = str.indexOf("w",2);//c = -1
5 int d = str.lastIndexOf("a");//d = 5
6 int e = str.lastIndexOf("a",3);//e = 2
```

7、字符串中字符的大小写转换 1)**public String toLowerCase()**//返回将当前字符串中所有字符转换成小写后的新串 2)**public String toUpperCase()**//返回将当前字符串中所有字符转换成大写后的新串 

```java
1 String str = new String("asDF");
2 String str1 = str.toLowerCase();//str1 = "asdf"
3 String str2 = str.toUpperCase();//str2 = "ASDF"
```

8、字符串中字符的替换 1)**public String replace(char oldChar, char newChar)**//用字符newChar替换当前字符串中所有的oldChar字符，并返回一个新的字符串。 2)**public String replaceFirst(String regex, String replacement)**//该方法用字符replacement的内容替换当前字符串中遇到的第一个和字符串regex相匹配的子串，应将新的字符串返回。 3)**public String replaceAll(String regex, String replacement)**//该方法用字符replacement的内容替换当前字符串中遇到的所有和字符串regex相匹配的子串，应将新的字符串返回。 

```java
1 String str = "asdzxcasd";
2 String str1 = str.replace('a','g');//str1 = "gsdzxcgsd"
3 String str2 = str.replace("asd","fgh");//str2 = "fghzxcfgh"
4 String str3 = str.replaceFirst("asd","fgh");//str3 = "fghzxcasd"
5 String str4 = str.replaceAll("asd","fgh");//str4 = "fghzxcfgh"
```

9、其他类方法 

1)**String trim()**//截去字符串两端的空格，但对于中间的空格不处理。 

```java
1 String str = " a sd ";
2 String str1 = str.trim();
3 int a = str.length();//a = 6
4 int b = str1.length();//b = 4
```

2)**boolean statWith(String prefix)**或**boolean endWith(String suffix)**//用来比较当前字符串的起始字符或子字符串prefix和终止字符或子字符串suffix是否和当前字符串相同，重载方法中同时还可以指定比较的开始位置offset。

```java
1 String str = "asdfgh";
2 boolean a = str.statWith("as");//a = true
3 boolean b = str.endWith("gh");//b = true
```

3)**regionMatches(boolean b, int firstStart, String other, int otherStart, int length)**//从当前字符串的firstStart位置开始比较，取长度为length的一个子字符串，other字符串从otherStart位置开始，指定另外一个长度为length的字符串，两字符串比较，当b为true时字符串不区分大小写。
4)**contains(String** **str)**//判断参数s是否被包含在字符串中，并返回一个布尔类型的值。

```java
1 String str = "student";
2 str.contains("stu");//true
3 str.contains("ok");//false
```

5)**String[] split(String str)**//将str作为分隔符进行字符串分解，分解后的字字符串在字符串数组中返回。

```java
1 String str = "asd!qwe|zxc#";
2 String[] str1 = str.split("!|#");//str1[0] = "asd";str1[1] = "qwe";str1[2] = "zxc";
```

#### 11. 抽象类必须要有抽象方法吗？

不需要，抽象类不一定非要有抽象方法。

#### 12. 普通类和抽象类有哪些区别？

- 普通类不能包含抽象方法，抽象类可以包含抽象方法。
- 抽象类不能直接实例化，普通类可以直接实例化。

#### 13. 抽象类能使用 final 修饰吗？

不能，定义抽象类就是让其他类继承的，如果定义为 final 该类就不能被继承，这样彼此就会产生矛盾，所以 final 不能修饰抽象类.

#### 14. 接口和抽象类有什么区别？

1. 接口能够多实现，而抽象类只能单独被继承，其本质就是，一个类能继承多个接口，而只能继承一个抽象类。
2. 方法上，抽象类的方法可以用abstract 和public或者protect修饰。而接口默认为public abstract 修饰。
3. 抽象类的方法可以有需要子类实现的抽象方法，也可以有具体的方法。而接口在老版本的jdk中，只能有抽象方法，但是Java8版本的接口中，接口可以带有默认方法。
4. 属性上，抽象类可以用各种各样的修饰符修饰。而接口的属性是默认的public static final
5. 抽象类可以含有构造方法，接口不能含有构造方法。
6. 设计层面上，抽象类表示的是子类“是不是”属于某一类的子类，接口则表示“有没有”特性“能不能”做这种事。如飞机和鸟都能飞，但是他们在设计上实现一个Fly接口，实现fly()方法。远比两个类继承飞行物抽象类好得多。因为，飞机和鸟有太多的属性不一样。
7. 设计层面上，另外一点，抽象类可以是一个模板，因为可以自己带集体方法，所以要加一个实现类都能有的方法，直接在抽象类中写出并实现就好，接口在以前的版本则不行。新版本Java8才有默认方法。
8. 既然说到Java 8 那么就来说明，Java8中的接口中的默认方法是可以被多重继承的。而抽象类不行。
9. 另外，接口只能继承接口。而抽象类可以继承普通的类，也能继承接口和抽象类。

#### 15. java 中 IO 流分为几种？

按功能来分：输入流（input）、输出流（output）。

按类型来分：字节流和字符流。

字节流和字符流的区别是：字节流按 8 位传输以字节为单位输入输出数据，字符流按 16 位传输以字符为单位输入输出数据。

#### 16. BIO、NIO、AIO 有什么区别？

- BIO：Block IO 同步阻塞式 IO，就是我们平常使用的传统 IO，它的特点是模式简单使用方便，并发处理能力低。
- NIO：New IO 同步非阻塞 IO，是传统 IO 的升级，客户端和服务器端通过 Channel（通道）通讯，实现了多路复用。
- AIO：Asynchronous IO 是 NIO 的升级，也叫 NIO2，实现了异步非堵塞 IO ，异步 IO 的操作基于事件和回调机制。

#### 17. Files的常用方法都有哪些？

- Files.exists()：检测文件路径是否存在。
- Files.createFile()：创建文件。
- Files.createDirectory()：创建文件夹。
- Files.delete()：删除一个文件或目录。
- Files.copy()：复制文件。
- Files.move()：移动文件。
- Files.size()：查看文件个数。
- Files.read()：读取文件。
- Files.write()：写入文件。



# 容器

#### 18. java 容器都有哪些？

![](http://ww1.sinaimg.cn/large/005WjvZYly1g1jkgb4a5cj30k00ehmx7.jpg)

#### 19. Collection 和 Collections 有什么区别？

java.util.Collection 是一个集合接口（集合类的一个顶级接口）。它提供了对集合对象进行基本操作的通用接口方法。Collection接口在Java 类库中有很多具体的实现。Collection接口的意义是为各种具体的集合提供了最大化的统一操作方式，其直接继承接口有List与Set。

Collections则是集合类的一个工具类/帮助类，其中提供了一系列静态方法，用于对集合中元素进行排序、搜索以及线程安全等各种操作。

#### 20. List、Set、Map 之间的区别是什么？

![](http://ww1.sinaimg.cn/large/005WjvZYly1g1jkjanc17j30nu0atwet.jpg)  

#### 21. HashMap 和 Hashtable 有什么区别？

hashMap去掉了HashTable 的contains方法，但是加上了containsValue（）和containsKey（）方法。

hashTable同步的，而HashMap是非同步的，效率上比hashTable要高。

hashMap允许空键值，而hashTable不允许。

#### 22. 如何决定使用 HashMap 还是 TreeMap？

对于在Map中插入、删除和定位元素这类操作，HashMap是最好的选择。然而，假如你需要对一个有序的key集合进行遍历，TreeMap是更好的选择。基于你的collection的大小，也许向HashMap中添加元素会更快，将map换为TreeMap进行有序key的遍历。

#### 23.说一下 HashMap 的实现原理？

HashMap概述： HashMap是基于哈希表的Map接口的非同步实现。此实现提供所有可选的映射操作，并允许使用null值和null键。此类不保证映射的顺序，特别是它不保证该顺序恒久不变。 

HashMap的数据结构： 在java编程语言中，最基本的结构就是两种，一个是数组，另外一个是模拟指针（引用），所有的数据结构都可以用这两个基本结构来构造的，HashMap也不例外。HashMap实际上是一个“链表散列”的数据结构，即数组和链表的结合体。

当我们往Hashmap中put元素时,首先根据key的hashcode重新计算hash值,根绝hash值得到这个元素在数组中的位置(下标),如果该数组在该位置上已经存放了其他元素,那么在这个位置上的元素将以链表的形式存放,新加入的放在链头,最先加入的放入链尾.如果数组中该位置没有元素,就直接将该元素放到数组的该位置上。

需要注意Jdk 1.8中对HashMap的实现做了优化,当链表中的节点数据超过八个之后,该链表会转为红黑树来提高查询效率,从原来的O(n)到O(logn)

#### 24. 说一下 HashSet 的实现原理？

- HashSet底层由HashMap实现
- HashSet的值存放于HashMap的key上
- HashMap的value统一为PRESENT

#### 25. ArrayList 和 LinkedList 的区别是什么？

最明显的区别是 ArrrayList底层的数据结构是数组，支持随机访问，而 LinkedList 的底层数据结构是双向循环链表，不支持随机访问。使用下标访问一个元素，ArrayList 的时间复杂度是 O(1)，而 LinkedList 是 O(n)。

#### 26. 如何实现数组和 List 之间的转换？

- List转换成为数组：调用ArrayList的toArray方法。
- 数组转换成为List：调用Arrays的asList方法。

#### 27. ArrayList 和 Vector 的区别是什么？

- Vector是同步的，而ArrayList不是。然而，如果你寻求在迭代的时候对列表进行改变，你应该使用CopyOnWriteArrayList。 
- ArrayList比Vector快，它因为有同步，不会过载。 
- ArrayList更加通用，因为我们可以使用Collections工具类轻易地获取同步列表和只读列表。

#### 28. Array 和 ArrayList 有何区别？

- Array可以容纳基本类型和对象，而ArrayList只能容纳对象。 
- Array是指定大小后不可变的，而ArrayList大小是可变的。 
- Array没有提供ArrayList那么多功能，比如addAll、removeAll和iterator等。

#### 29. 在 Queue 中 poll()和 remove()有什么区别？

poll() 和 remove() 都是从队列中取出一个元素，但是 poll() 在获取元素失败的时候会返回空，但是 remove() 失败的时候会抛出异常。

#### 30. 哪些集合类是线程安全的？

- vector：就比arraylist多了个同步化机制（线程安全），因为效率较低，现在已经不太建议使用。在web应用中，特别是前台页面，往往效率（页面响应速度）是优先考虑的。
- statck：堆栈类，先进后出。
- hashtable：就比hashmap多了个线程安全。
- enumeration：枚举，相当于迭代器。

#### 31. 迭代器 Iterator 是什么？

迭代器是一种设计模式，它是一个对象，它可以遍历并选择序列中的对象，而开发人员不需要了解该序列的底层结构。迭代器通常被称为“轻量级”对象，因为创建它的代价小。

#### 32. Iterator 怎么使用？有什么特点？

Java中的Iterator功能比较简单，并且只能单向移动：

(1) 使用方法iterator()要求容器返回一个Iterator。第一次调用Iterator的next()方法时，它返回序列的第一个元素。注意：iterator()方法是java.lang.Iterable接口,被Collection继承。

(2) 使用next()获得序列中的下一个元素。

(3) 使用hasNext()检查序列中是否还有元素。

(4) 使用remove()将迭代器新返回的元素删除。　

Iterator是Java迭代器最简单的实现，为List设计的ListIterator具有更多的功能，它可以从两个方向遍历List，也可以从List中插入和删除元素。



#### 33. Iterator 和 ListIterator 有什么区别？

- Iterator可用来遍历Set和List集合，但是ListIterator只能用来遍历List。 
- Iterator对集合只能是前向遍历，ListIterator既可以前向也可以后向。 
- ListIterator实现了Iterator接口，并包含其他的功能，比如：增加元素，替换元素，获取前一个和后一个元素的索引，等等。