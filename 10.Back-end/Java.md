# Java：

Java是由Sun Microsystems公司于1995年5月推出的Java面向对象程序设计语言和Java平台的总称。由James Gosling和同事们共同研发，并在1995年正式推出。Java编程语言的风格十分接近C++语言。继承了C++语言面向对象技术的核心，Java舍弃了C++语言中容易引起错误的指针，改以引用取代，同时移除原C++与原来运算符重载，也移除多重继承特性，改用接口取代，增加垃圾回收器功能。在Java SE 1.5版本中引入了泛型编程、类型安全的枚举、不定长参数和自动装/拆箱特性。太阳微系统对Java语言的解释是："Java编程语言是个简单、面向对象、分布式、解释性、健壮、安全与系统无关、可移植、高性能、多线程和动态的语言"。

Java不同于一般的编译语言或直译语言。它首先将源代码编译成字节码，然后依赖各种不同平台上的虚拟机来解释执行字节码，从而实现了"一次编写，到处运行"的跨平台特性。在早期JVM中，这在一定程度上降低了Java程序的运行效率。但在J2SE1.4.2发布后，Java的运行速度有了大幅提升。执行Java应用程序必须安装爪哇运行环境（Java Runtime Environment，JRE），JRE内部有一个Java虚拟机（Java Virtual Machine，JVM）以及一些标准的类库（Class Library）。通过JVM才能在电脑系统执行Java应用程序（Java Application），这与.Net Framework的情况一样，所以电脑上没有安装JVM，那么这些程序将不能够执行。 实现跨平台性的方法是大多数编译器在进行Java语言程序的编码时候会生成一个用字节码写成的"半成品"，这个"半成品"会在Java虚拟机（解释层）的帮助下运行，虚拟机会把它转换成当前所处硬件平台的原始代码。之后，Java虚拟机会打开标准库，进行数据（图片、线程和网络）的访问工作。主要注意的是，尽管已经存在一个进行代码翻译的解释层，有些时候Java的字节码代码还是会被JIT编译器进行二次编译。 C++语言被用户诟病的原因之一是大多数C++编译器不支持垃圾收集机制。通常使用C++编程的时候，程序员于程序中初始化对象时，会在主机内存堆栈上分配一块内存与地址，当不需要此对象时，进行析构或者删除的时候再释放分配的内存地址。如果对象是在堆栈上分配的，而程序员又忘记进行删除，那么就会造成内存泄漏（Memory Leak）。长此以往，程序运行的时候可能会生成很多不清除的垃圾，浪费了不必要的内存空间。而且如果同一内存地址被删除两次的话，程序会变得不稳定，甚至崩溃。因此有经验的C++程序员都会在删除之后将指针重置为NULL，然后在删除之前先判断指针是否为NULL。 C++中也可以使用"智能指针"（Smart Pointer）或者使用C++托管扩展编译器的方法来实现自动化内存释放，智能指针可以在标准类库中找到，而C++托管扩展被微软的Visual C++ 7.0及以上版本所支持。智能指针的优点是不需引入缓慢的垃圾收集机制，而且可以不考虑线程安全的问题，但是缺点是如果不善使用智能指针的话，性能有可能不如垃圾收集机制，而且不断地分配和释放内存可能造成内存碎片，需要手动对堆进行压缩。除此之外，由于智能指针是一个基于模板的功能，所以没有经验的程序员在需要使用多态特性进行自动清理时也可能束手无策。 Java语言则不同，上述的情况被自动垃圾收集功能自动处理。对象的创建和放置都是在内存堆栈上面进行的。当一个对象没有任何引用的时候，Java的自动垃圾收集机制就发挥作用，自动删除这个对象所占用的空间，释放内存以避免内存泄漏。

- JavaSE（J2SE）（Java2 Platform Standard Edition，java平台标准版）
- JavaEE(J2EE)(Java 2 Platform,Enterprise Edition，java平台企业版)
- JavaME(J2ME)(Java 2 Platform Micro Edition，java平台微型版)。

资源包(<http://www.oracle.com/technetwork/java/javase/downloads/index.html>)

JDK：Java Development Kit

JRE: Java Runtime Environment

# [安装教程](https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-get-on-debian-8)类debian系统

```
# using the version packaged with Debian：OpenJDK 8
sudo apt-get update
sudo apt-get install default-jre
# JDK 包含JRE
sudo apt-get install default-jdk

# Installing the Oracle JDK
sudo apt-get install software-properties-common
sudo add-apt-repository "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main"
sudo apt-get update
sudo apt-get install oracle-java8-installer
javac -version

sudo apt-get install oracle-java9-installer
# 多版本管理
sudo update-alternatives --config java | javac 会获得程序路径
```

# JAVA_HOME Environment Variable配置

```
sudo vim /etc/environment 添加 JAVA_HOME="/usr/lib/jvm/java-8-oracle"
source /etc/environment
echo $JAVA_HOME
```

# 例子

```
新建文件 HelloWorld.java
public class HelloWorld {
    /* 第一个Java程序
     * 它将打印字符串 Hello World
     */
    public static void main(String []args) {
        System.out.println("Hello World"); // 打印 Hello World
    }
}
# 编译
javac HelloWorld.java
# 运行
java HelloWorld
```

## maven

```
sudo apt-get install maven2
```

## todo

Hadoop，Kafka，Zookeeper