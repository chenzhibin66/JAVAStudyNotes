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

#### 34.怎么确保一个集合不能被修改？

# 多线程

#### 35.并行和并发有什么区别？

- 并发在单核和多核都可存在，就是同一时间有多个可以执行的进程。但是在单核中同一时刻只有一个进程获得CPU,虽然宏观上你认为多个进程都在进行
- 并行是指同一时间多个进程在微观上都在真正的执行，这就只有在多核的情况下了

#### 36.线程和进程的区别？

- 线程：是程序执行流的最小单元，是系统独立调度和分配CPU（独立运行）的基本单位
- 进程：是资源分配的基本单位。一个进程包括多个线程

区别：地址空间、资源拥有

1. 线程与资源分配无关，它属于某一个进程，并与进程内的其他线程一起共享进程的资源
2. 每个进程都有自己一套独立的资源（数据），供其内的所有线程共享
3. 不论是大小，开销线程要更“轻量级”
4. 一个进程内的线程通信比进程之间的通信更快速，有效。（因为共享变量）

#### 37.守护线程是什么？

答：守护线程是个服务线程，服务于其他线程

典型案例：垃圾回收线程

#### 38.创建线程有哪几种方式？

答：

- 继承Threa类创建线程
- 实现Runnable接口创建线程
- 通过Callable和Future创建线程

#### 39.说一下 runnable 和 callable 有什么区别？

答：runnable 没有返回值，callable 可以拿到有返回值，callable 可以看作是 runnable 的补充。

#### 40.线程有哪些状态？

答：创建、就绪、运行、阻塞、死亡

#### 41.sleep() 和 wait() 有什么区别？

 答：

- sleep() 可以在任何地方使用
- wait() 只能在同步方法或同步块中使用

#### 42.notify()和 notifyAll()有什么区别？

答：

- notify是唤醒某个线程
- notifyAll是唤醒所有暂停线程

#### 43.线程的 run()和 start()有什么区别？

- run() 相当于线程的任务处理逻辑的入口方法
- start() 的作用是启动相应的线程

#### 44.创建线程池有哪几种方式？

线程池创建有七种方式，最核心的是最后一种：

- newSingleThreadExecutor()：它的特点在于工作线程数目被限制为 1，操作一个无界的工作队列，所以它保证了所有任务的都是被顺序执行，最多会有一个任务处于活动状态，并且不允许使用者改动线程池实例，因此可以避免其改变线程数目；
- newCachedThreadPool()：它是一种用来处理大量短时间工作任务的线程池，具有几个鲜明特点：它会试图缓存线程并重用，当无缓存线程可用时，就会创建新的工作线程；如果线程闲置的时间超过 60 秒，则被终止并移出缓存；长时间闲置时，这种线程池，不会消耗什么资源。其内部使用 SynchronousQueue 作为工作队列；
- newFixedThreadPool(int nThreads)：重用指定数目（nThreads）的线程，其背后使用的是无界的工作队列，任何时候最多有 nThreads 个工作线程是活动的。这意味着，如果任务数量超过了活动队列数目，将在工作队列中等待空闲线程出现；如果有工作线程退出，将会有新的工作线程被创建，以补足指定的数目 nThreads；
- newSingleThreadScheduledExecutor()：创建单线程池，返回 ScheduledExecutorService，可以进行定时或周期性的工作调度；
- newScheduledThreadPool(int corePoolSize)：和newSingleThreadScheduledExecutor()类似，创建的是个 ScheduledExecutorService，可以进行定时或周期性的工作调度，区别在于单一工作线程还是多个工作线程；
- newWorkStealingPool(int parallelism)：这是一个经常被人忽略的线程池，Java 8 才加入这个创建方法，其内部会构建ForkJoinPool，利用Work-Stealing算法，并行地处理任务，不保证处理顺序；
- ThreadPoolExecutor()：是最原始的线程池创建，上面1-3创建方式都是对ThreadPoolExecutor的封装。

#### 45.线程池都有哪些状态？

- RUNNING：这是最正常的状态，接受新的任务，处理等待队列中的任务。
- SHUTDOWN：不接受新的任务提交，但是会继续处理等待队列中的任务。
- STOP：不接受新的任务提交，不再处理等待队列中的任务，中断正在执行任务的线程。
- TIDYING：所有的任务都销毁了，workCount 为 0，线程池的状态在转换为 TIDYING 状态时，会执行钩子方法 terminated()。
- TERMINATED：terminated()方法结束后，线程池的状态就会变成这个。

#### 46.线程池中 submit()和 execute()方法有什么区别？

- execute()：只能执行 Runnable 类型的任务。
- submit()：可以执行 Runnable 和 Callable 类型的任务。

Callable 类型的任务可以获取执行的返回值，而 Runnable 执行无返回值。

#### 47.在 java 程序中怎么保证多线程的运行安全？

- 方法一：使用安全类，比如 Java. util. concurrent 下的类。
- 方法二：使用自动锁 synchronized。
- 方法三：使用手动锁 Lock。

手动锁Java示例代码如下：

```java
Lock lock = new ReentrantLock();
lock.lock();
try {
    System. out. println("获得锁");
} catch (Exception e) {
    // TODO: handle exception
} finally {
    System. out. println("释放锁");
    lock. unlock();
}
```

#### 48.多线程锁的升级原理是什么？

答：

synchronized 锁升级原理：在锁对象的对象头里面有一个 threadid 字段，在第一次访问的时候 threadid 为空，jvm 让其持有偏向锁，并将 threadid 设置为其线程 id，再次进入的时候会先判断 threadid 是否与其线程 id 一致，如果一致则可以直接使用此对象，如果不一致，则升级偏向锁为轻量级锁，通过自旋循环一定次数来获取锁，执行一定次数之后，如果还没有正常获取到要使用的对象，此时就会把锁从轻量级升级为重量级锁，此过程就构成了 synchronized 锁的升级。

锁的升级的目的：锁升级是为了减低了锁带来的性能消耗。在 Java 6 之后优化 synchronized 的实现方式，使用了偏向锁升级为轻量级锁再升级到重量级锁的方式，从而减低了锁带来的性能消耗。

#### 49.什么是死锁？

答：当线程 A 持有独占锁a，并尝试去获取独占锁 b 的同时，线程 B 持有独占锁 b，并尝试获取独占锁 a 的情况下，就会发生 AB 两个线程由于互相持有对方需要的锁，而发生的阻塞现象，我们称为死锁。

#### 50.怎么防止死锁？

答：

- 尽量使用 tryLock(long timeout, TimeUnit unit)的方法(ReentrantLock、ReentrantReadWriteLock)，设置超时时间，超时可以退出防止死锁。
- 尽量使用 Java. util. concurrent 并发类代替自己手写锁。
- 尽量降低锁的使用粒度，尽量不要几个功能用同一把锁。
- 尽量减少同步的代码块。

#### 51.ThreadLocal 是什么？有哪些使用场景？

答：ThreadLocal用于保存某个线程共享变量。使用场景：解决数据库连接，Session管理

#### 52.说一下 synchronized 底层实现原理？

答：synchronized 是由一对 monitorenter/monitorexit 指令实现的，monitor 对象是同步的基本实现单元。在 Java 6 之前，monitor 的实现完全是依靠操作系统内部的互斥锁，因为需要进行用户态到内核态的切换，所以同步操作是一个无差别的重量级操作，性能也很低。但在 Java 6 的时候，Java 虚拟机 对此进行了大刀阔斧地改进，提供了三种不同的 monitor 实现，也就是常说的三种不同的锁：偏向锁（Biased Locking）、轻量级锁和重量级锁，大大改进了其性能。

#### 53.synchronized 和 volatile 的区别是什么？

答：

- volatile 是变量修饰符；synchronized 是修饰类、方法、代码段。
- volatile 仅能实现变量的修改可见性，不能保证原子性；而 synchronized 则可以保证变量的修改可见性和原子性。
- volatile 不会造成线程的阻塞；synchronized 可能会造成线程的阻塞。

#### 54.synchronized 和 Lock 有什么区别？

- synchronized 可以给类、方法、代码块加锁；而 lock 只能给代码块加锁。
- synchronized 不需要手动获取锁和释放锁，使用简单，发生异常会自动释放锁，不会造成死锁；而 lock 需要自己加锁和释放锁，如果使用不当没有 unLock()去释放锁就会造成死锁。
- 通过 Lock 可以知道有没有成功获取锁，而 synchronized 却无法办到。

#### 55.synchronized 和 ReentrantLock 区别是什么？

答：

synchronized 早期的实现比较低效，对比 ReentrantLock，大多数场景性能都相差较大，但是在 Java 6 中对 synchronized 进行了非常多的改进。

主要区别如下：

- ReentrantLock 使用起来比较灵活，但是必须有释放锁的配合动作；
- ReentrantLock 必须手动获取与释放锁，而 synchronized 不需要手动释放和开启锁；
- ReentrantLock 只适用于代码块锁，而 synchronized 可用于修饰方法、代码块等。
- volatile 标记的变量不会被编译器优化；synchronized 标记的变量可以被编译器优化。

#### 56.说一下 atomic 的原理？

答：atomic 主要利用 CAS (Compare And Wwap) 和 volatile 和 native 方法来保证原子操作，从而避免 synchronized 的高开销，执行效率大为提升。