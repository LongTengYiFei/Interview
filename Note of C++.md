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



### protected



### int64_t and int32_t



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



### printf/vprintf



### fflush and fsync

https://stackoverflow.com/questions/2340610/difference-between-fflush-and-fsync



### typename and class

https://stackoverflow.com/questions/2023977/difference-of-keywords-typename-and-class-in-templates
