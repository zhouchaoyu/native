Java 调用本地代码之native
h3.

简述： 

     Java语言中的native关键字，以及Java语言调用C语言的编译生成本地动态链接库(DLL)示例。 
     一. 什么是JNI
　　JNI是Java Native Interface的缩写，它提供了若干的API实现了Java和其他语言的通信（主要是C&C++）。从Java1.1开始，JNI标准成为java平台的一部分，它允许Java代码和其他语言写的代码进行交互。JNI一开始是为了本地已编译语言，尤其是C和C++而设计的，但是它并不妨碍你使用其他编程语言，只要调用约定受支持就可以了。使用java与本地已编译的代码交互，通常会丧失平台可移植性。但是，有些情况下这样做是可以接受的，甚至是必须的。例如，使用一些旧的库，与硬件、操作系统进行交互，或者为了提高程序的性能。JNI标准至少要保证本地代码能工作在任何Java 虚拟机环境下。

　　总的来说，JNI就是一个允许Java语言和其他编程语言(主要是C/C++)通信的接口。C/C++是系统级的编程语言, 可以用来开发任何和系统相关的程序和类库, 但是Java本身编写底层的应用比较难实现, 使用JNI可以调用现有的本地库, 极大地灵活了Java的开发. C/C++的效率是目前最好的语言, 可以使用C/C++来实现一些实时性非常高的部分. C/C++和Java本身都是非常流行的编程语言, 一些大型软件中经常使用语言之间的混合编程.

　　一旦使用JNI, JAVA程序就丧失了JAVA平台的两个优点: 程序不在跨平台。要想跨平台，必须在不同的系统环境中重新编译本地语言部分；程序不再是绝对安全的，本地代码的不当使用可能导致整个陈旭崩溃。一个通用的规则是，你应该让本地方法集中在少数几个类当中，这样就降低了Java语言和C/C++之间的耦合性。

　　使用JNI实现Java与C语言混合编程的基本步骤如下：

       1. 编写带有native声明的方法的java类
       2.使用javac命令编译所有的java类
       3.然后使用javah + 类名生成扩展名为.h的头文件
       4.使用C/C++实现本地方法
       5.将C/C++编写的文件生成动态链接库
       6. java加载此链接库 

代码示例： 

         第一步编写：java native 方法
          public class NativeMethod {

     public static void main(String[] args)
        { 

            System.loadLibrary("Tool"); 
            NativeMethodLoader nmt = new NativeMethodLoader();
            Double double1 = Double.valueOf(args[0]);
            Double double2 = Double.valueOf(args[1]);
            System.out.println(double1+"----------------"+double2);
            double add = nmt.Add(double1,double2);
            System.out.println(add);

        }

    static class NativeMethodLoader
    {   
       public native double Add(double x,double y);
    }

}
        2.编译java 生成class文件       
        3. 生成.h文件
        。。。。。。。。。
        4. 实现底层代码生成dll链接库
        5. 将dll拷贝到classpath下

编辑此区域
运行结果：

      C:\Users\mayn\Desktop\nativeMethod>java NativeMethod 8 9
8.0----------------9.0
17.0

C:\Users\mayn\Desktop\nativeMethod>java NativeMethod 100000 9999
100000.0----------------9999.0
109999.0

C:\Users\mayn\Desktop\nativeMethod>java NativeMethod 1000000000000000000 9999
1.0E18----------------9999.0
1.00000000000000998E18

C:\Users\mayn\Desktop\nativeMethod>