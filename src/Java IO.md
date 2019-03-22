# Java IO

为了方面理解和阐述,先引入两张图:

​           a. java IO中常用的类

![](http://ww1.sinaimg.cn/large/005WjvZYly1g1b9r48x6rj30c505cmx3.jpg)

​      在整个java.io包中最重要的就是5个类和一个借口.5个类指的是File、OutputStream、InputStream、Writer、Reader;一个接口指的是Serializable,掌握了这些IO的核心操作那么对于java中的IO体系也有了一个初步的认识了



Java  I/O主要包括如下几个层次,包含三个部分:

1. 流式部分  - - -IO的主体部分;
2. 非流式部分 - - -主要包含一些辅助流式部分的类,如File类、RandomAccessFile类和FileDescriptor等类;
3. 其他类 - - -文件读取不分的与安全相关的类,如SerializeblePermission类,以及与本地操作系统相关的文件系统的类,如:FileSystem类和Win32FileSystem类和WinNTFileSystem类.



主要的类如下:

1. File(文件特征与管理):用于文件或者目录的描述信息,例如生成新目录,修改文件名,删除文件,判断文件所在路径等.
2. InputStream(二进制格式操作):抽象类,基于字节的输入操作,是所有输入流的父类.定义了所有输入流所具有的共同特征.
3. OutputStream(二级制格式操作):抽象类.基于字节的输出操作,是所有输出流的父类.定义了所有输出流都具有的共同特征.
4. Reader(文件格式操作):抽象类:基于字符的输入操作.
5. Writer(文件格式操作):抽象类:基于字符的输出操作.
6. RandomAccessFile(随机文件操作):一个独立的类,直接继承Object,它的功能丰富,可以从文件的任意位置进行存取(输入输出)操作.



Java中IO流的体系结构:

![](http://ww1.sinaimg.cn/large/005WjvZYly1g1ba5b7pzjj30fi09p76l.jpg)



b、Java流类的类结构图

![](http://ww1.sinaimg.cn/large/005WjvZYly1g1ba6g8pmmj30fi0b50vo.jpg)



### 1.流的概念和作用

流:代表任何有能力产出数据的数据源对象或者是有能力接受数据的接收端对象<Thinking in java>

流的本质:数据传输,根据数据传输特许将流抽象为各种累,方便更直观的进行数据操作.

### 2.IO流的分类

根据处理数据类型的不同分为：字符流和字节流

根据数据流向不同分为：输入流和输出流

按数据来源（去向）分类： 

1. File（文件）： FileInputStream, FileOutputStream, FileReader, FileWriter  
2. byte[]：ByteArrayInputStream, ByteArrayOutputStream  
3. Char[]: CharArrayReader,CharArrayWriter  
4. String:StringBufferInputStream, StringReader, StringWriter  
5. 网络数据流：InputStream,OutputStream, Reader, Writer  



### 字符流和字节流

流序列中的数据既可以是未经加工的原始二进制数据，也可以是经一定编码处理后符合某种格式规定的特定数据。因此Java中的流分为两种：

1. **字节流：**数据流中最小的数据单元是字节 
2. **字符流：**数据流中最小的数据单元是字符， Java中的字符是Unicode编码，一个字符占用两个字节。 

### 输入流和输出流

根据数据的输入、输出方向的不同对而将流分为输入流和输出流。 

1. ### **输入流**

   程序从输入流读取数据源。数据源包括外界(键盘、文件、网络…)，即是将数据源读入到程序的通信通道 

2. ### 输出流

   程序向输出流写入数据。将程序中的数据输出到外界（显示器、打印机、文件、网络…）的通信通道。 

   

   采用数据流的目的就是使得输出输入独立于设备。

   输入流( Input  Stream )不关心数据源来自何种设备（键盘，文件，网络）。
   输出流( Output Stream )不关心数据的目的是何种设备（键盘，文件，网络）。

3. ### **特性**

   相对于程序来说，输出流是往存储介质或数据通道写入数据，而输入流是从存储介质或数据通道中读取数据，一般来说关于流的特性有下面几点： 

   1. 先进先出，最先写入输出流的数据最先被输入流读取到。 
   2. 顺序存取，可以一个接一个地往流中写入一串字节，读出时也将按写入顺序读取一串字节，不能随机访问中间的数据。（RandomAccessFile**可以从文件的任意位置进行存取（输入输出）操作**） 
   3. 只读或只写，每个流只能是输入流或输出流的一种，不能同时具备两个功能，输入流只能进行读操作，对输出流只能进行写操作。在一个数据传输通道中，如果既要写入数据，又要读取数据，则要分别提供两个流。  



代码实例:



```java
public class main {
    public static void main(String[] args) {
        File file1 = new File("C:\\Users\\Administrator\\Desktop\\test.txt");
        File file2 = new File("C:\\Users\\Administrator\\Desktop\\test2.txt");
        readFile(file1);
        writeFile(file2);
        writeOneToAnother(file1, file2);

    }

    //从本地读取文件
    public static void readFile(File file) {
        BufferedInputStream in = null;
        try {
            in = new BufferedInputStream(new FileInputStream(file));
            byte[] bytes = new byte[1024];
            int n = in.read(bytes, 0, bytes.length);
            String str = new String(bytes, 0, n, "GBK");
            System.out.println(str);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }


    //从电脑输入写入文件
    public static void writeFile(File file) {
        BufferedOutputStream out = null;
        try {
            if (!file.exists()) {
                file.createNewFile();
            }
            out = new BufferedOutputStream(new FileOutputStream(file));
            Scanner sc = new Scanner(System.in);
            String s = sc.nextLine();
            byte[] bytes = s.getBytes();
            out.write(bytes, 0, bytes.length);
            out.flush();
            out.close();

        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    //将文件1的内容写入到文件2,会覆盖原来的内容
    public static void writeOneToAnother(File file1, File file2) {
        try {
            BufferedInputStream in = new BufferedInputStream(new FileInputStream(file1));
            BufferedOutputStream out = new BufferedOutputStream(new FileOutputStream(file2));
            byte[] bytes = new byte[1024];
            int n = in.read(bytes, 0, bytes.length);
            String s = new String(bytes, 0, n, "GBK");
            out.write(s.getBytes(), 0, s.getBytes().length);
            out.flush();
            out.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```