# Note of C++

### Function signature

Without parameter names, like this:

```c++
int foo(char*);
```



A function's **signature** includes the function's name and the number, order and type of its formal parameters.

Two overloaded functions must not have the same signature

The return value is **not** part of a function's signature

These two functions have the same signature

```c++
int Divide (int n, int m) ;
double Divide (int n, int m) ;
```

### Overloading Functions

[overloading functions URL](https://www.csee.umbc.edu/courses/undergraduate/202/spring07/Lectures/ChangSynopses/modules/m04-overload/slides.php?print)


### pragma once

Using `#pragma once` allows the [C preprocessor](https://en.wikipedia.org/wiki/C_preprocessor) to include a header file when it is needed and to ignore an `#include` directive otherwise. This has the effect of altering the behavior of the [C preprocessor](https://en.wikipedia.org/wiki/C_preprocessor) itself, and allows programmers to express file dependencies in a simple fashion, obviating the need for manual management.

https://en.wikipedia.org/wiki/Pragma_once


### strncmp

https://www.runoob.com/cprogramming/c-function-strncmp.html


### Argc and Argv

https://stackoverflow.com/questions/3024197/what-does-int-argc-char-argv-mean


### multi-line define

https://stackoverflow.com/questions/6281368/multi-line-define-directives


### assert

http://www.cplusplus.com/reference/cassert/assert/

我们可以在编译时指定assert是否crash进程


### extern

https://stackoverflow.com/questions/10422034/when-to-use-extern-in-c


### __thread

https://www.jianshu.com/p/997b533842c8

https://stackoverflow.com/questions/32245103/how-does-the-gcc-thread-work


### 存储类说明符

https://zh.cppreference.com/w/cpp/language/storage_duration


### 可变参数/变参宏

https://www.cnblogs.com/hanyonglu/archive/2011/05/07/2039916.html

https://blog.csdn.net/u012707739/article/details/80170671

[对于可变参数为空情形，Visual Studio直接去掉可变参数前面的逗号，GCC需要在\_\_VA_\_ARGS__前面放上##以去除逗号。](https://blog.csdn.net/fengbingchun/article/details/78483471)


### printf 合并字符串

https://blog.csdn.net/yanxiaolx/article/details/51531633


### fflush and fsync

https://stackoverflow.com/questions/2340610/difference-between-fflush-and-fsync


### typename and class

https://stackoverflow.com/questions/2023977/difference-of-keywords-typename-and-class-in-templates



### c有重载吗

c语言是没有重载的，重载需要编译器的支持，c++编译器会对函数名加前缀和后缀来修饰函数名，可以用readelf或者nm命令来查看编译后的目标文件。

c语言的目标文件，函数名是没有修饰的，而c++的函数名在目标文件中是加了前缀和后缀修饰过的。

关于函数签名和符号修饰可以阅读《程序员的自我修养》。



### c/c++区别

c++支持面向对象，继承，封装，多态。

c++面向对象，c面向过程。

c++数据和函数被封装在对象里。c的函数和数据是分开的。



### c++如何调用c

用extern "C"，

被它大括号括住的函数声明，将不会使用c++的符号修饰。详情见《程序员的自我修养》。

举个例子：

```c
// test2.h

int add(int, int);
```

```c
// test2.c

int add(int a, int b)

{

​	return a+b;

}
```

```c++
// test1.cpp

#include <test2.h>

int main()
{
	add(10, 20);
}
/*
这个时候你如果编译链接，是会失败的，会告诉你main函数里面使用了未定义的add，但是add不是已经命名被定义过了吗？
在test1.cpp里面，add会被符号修饰，可以gcc test1.cpp -c ，然后用nm命令查看test1.o里面的符号，发现add已经被修饰过了。
而我们的add的定义是在c文件里的，是c语言，c的编译是不会有符号修饰的。
我这里试验时修饰后的符号是"_Z3addii"，单独编译test2.c后add符号就是"add"，没有任何修饰，所以链接时，寻找"_Z3addii"的定义，是找不到的。
add 在test1.cpp里只是声明。
*/
```

```c++
// test1.cpp
extern "C"{
#include <test2.h>
}
int main()
{
	add(10, 20);
}
/*
这时，test1.cpp里的add声明被extern "C"括起来了，编译器就把它当做c代码处理，不会对其进行符号修饰。test1.o里的add符号就是"add"。
test2.o里的add也还是"add"，所以函数定义就能找到了。
*/
```



### 多态-what/why/how

多态的意思就是相同的实体，在不同场合下有不同的表现。对象/函数。

编译时：函数重载，运算符重载(也是函数重载的一种)

函数重载：虽然函数名相同，但是参数列表不同。

运算符重载：同理，虽然同是一个运算符，但参数列表不同。

运行时：虚函数



### 虚函数- what/why/how 

用父类指针指向子类对象，调用虚函数，调用的版本是子类重写的版本（如果子类重写了的话）。

多态的一种实现方式。



### 虚表(virtual table)



### 虚析构函数

https://blog.csdn.net/weicao1990/article/details/81911341

只有当一个类被用来作为基类的时候，才把析构函数写成虚函数。



### 纯虚函数



### 栈溢出/堆溢出

堆实际上是没办法溢出的，当我们申请的空间大于堆上限时，malloc直接返回空指针。

如果用new，则会抛出异常 std::bad_alloc。

```c++
#include <stdio.h>
#include <stdlib.h>
int main(int argc, char const* argv[])
{
     int a[999999999999999];
     printf("%x\n", a);
}
/*
栈溢出
执行结果是Segmentation fault (core dumped)
*/
```

```c++
#include <stdio.h>
#include <stdlib.h>
int main(int argc, char const* argv[])
{
     int *a = new int[99999999999];
     printf("%x\n", a);
}
/*
执行结果是
terminate called after throwing an instance of 'std::bad_alloc'
  what():  std::bad_alloc
Aborted (core dumped)
*/
```

```c++
#include <stdio.h>
#include <stdlib.h>
int main(int argc, char const* argv[])
{
     int *a = (int*)malloc(99999999999);
     printf("%x\n", a);
}
/*
执行结果是0，malloc失败。
*/
```



### New and malloc

1.对于申请超过限制的空间，结果不同，new是抛出异常，malloc则是返回空指针。

2.new会调用对象的构造函数，而malloc只是单纯的分配空间。

3.new返回特定对象的指针，而malloc返回空指针，就是个地址，一般用的时候要强制转换一下。

4.new是运算符，而malloc只是个函数。

5.new一个对象的时候编译器帮我们计算所需空间，而malloc需要我们自己计算所需空间大小（一般用sizeof）。

6.new从自由存储区获取空间，malloc从堆获取空间（自由存储区和堆是不能划等号的！！！难点！！！）

7.



### FREE STORE vs HEAP
自由存储区可以理解为一块空闲的区域，可以是堆，也可以是别的地方。
通过重载new操作符，可以自定义，从哪里获取空间。
就比方说，一个类的静态成员变量是一个数组，我们用这个数组来当作自由存储区，然后重载这个类的new，让new从这个数组里获取空间。
具体可以参考《c++编程思想》p326-p328.

### Const cast- what/why/how

### Static cast- what/why/how

### Reinterpret cast - what/why/how

### Dynamic cast - what/why/how

### smart pointer- what/why/how

### iterator- what/why/how

### 求二叉树深度

### STL

### 设计模式


