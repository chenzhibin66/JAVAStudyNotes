JAVA序列化

Java提供了一种对象序列化的机制，一个对象可以被表示为一个字节序列，该字节序列包括该对象的数据、有关对象的类型的信息和存储在对象中数据的类型。

将序列化对象写入文件后，可以从文件中读取出来，并且对它进行反序列化，也就是说，对象的类型信息、对象的数据，还有对象中的数据类型可以用来在内存中新建对象。

Employee对象：

```java
public class Employee implements Serializable {
    public String name;
    public String address;
    public transient int SSN;
    public int number;

    public void mailCheck() {
        System.out.println("Mailing a check to" + name + "" + address);
    }
}
```

序列化对象：

```java
public class SerializeDemo {
    public static void main(String[] args) {
        Employee e = new Employee();
        e.name = "Calvin";
        e.address = "nuc";
        e.SSN = 11122333;
        e.number = 101;
        try {
            FileOutputStream fileOutputStream = new FileOutputStream("C:\\Users\\Administrator\\Desktop\\employee.ser");
            ObjectOutputStream out = new ObjectOutputStream(fileOutputStream);
            out.writeObject(e);
            out.close();
            fileOutputStream.close();
            System.out.println("Serialized data is saved");
        } catch (IOException i) {
            i.printStackTrace();
        }
    }
}
```

反序列化对象：

```java
public class SerializeDemo {
    public static void main(String[] args) {
        Employee e = null;
        try {
            FileInputStream fileInputStream = new FileInputStream("C:\\Users\\Administrator\\Desktop\\employee.ser");
            ObjectInputStream in = new ObjectInputStream(fileInputStream);
            e = (Employee) in.readObject();
        } catch (IOException i) {
            i.printStackTrace();
        } catch (ClassNotFoundException c) {
            System.out.println("Employee class not found");
            c.printStackTrace();
            return;
        }
        System.out.println("Deserialized Employee....");
        System.out.println("Name" + e.name);
        System.out.println("Address" + e.address);
        System.out.println("SSN" + e.SSN);
        System.out.println("Number" + e.number);
    }
}
```

![](http://ww1.sinaimg.cn/large/abef3392ly1g2kgbnnrjvj20lf07jgly.jpg)

这里要注意以下要点：

readObject() 方法中的 try/catch代码块尝试捕获 ClassNotFoundException 异常。对于 JVM 可以反序列化对象，它必须是能够找到字节码的类。如果JVM在反序列化对象的过程中找不到该类，则抛出一个 ClassNotFoundException 异常。

注意，readObject() 方法的返回值被转化成 Employee 引用。

当对象被序列化时，属性 SSN 的值为 111222333，但是因为该属性是短暂的，该值没有被发送到输出流。所以反序列化后 Employee 对象的 SSN 属性为 0。