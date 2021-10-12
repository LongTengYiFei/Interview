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

