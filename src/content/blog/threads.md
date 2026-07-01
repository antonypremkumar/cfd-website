---
title: 'Multithreading'
description: 'Parallelism'
pubDate: 'Jul 01 2026'
heroImage: '../../assets/threads.png'
---

Until C++11, parallelism was possible only using the API provided by the operating system.
In the case of linux, `pthreads` were used.
From C++11 onwards multithreading is possible using the thread api.

```
#include<iostream>
#include<thread>

void hello() {
  std::cout << "Hi there" << std::endl;
}

int main() {
  std::thread t1 {hello}; 
  t1.join();
  return 0;
}
```

One has to include the `thread` library. 
An object of the class `std::thread` has to be created with a function.
The function could be a 

- function pointer
- lambda function or
- function object

You can for example run this using the following command

```
clang++ -g -std=c++20 -pthread -Wall -Wextra simple.cpp -o simple
```

When you use `gdb` to step through the function one can see the two threads.

```
Thread 2 "simple" hit Breakpoint 2, hello () at simple.cpp:6
6         std::cout << "Hi there" << std::endl;
(gdb) info threads
  Id   Target Id                                   Frame 
  1    Thread 0x7ffff7e95740 (LWP 107927) "simple" 0x00007ffff7898d71 in __futex_abstimed_wait_common64 (private=128, cancel=true, 
    abstime=0x0, op=265, expected=107977, futex_word=0x7ffff77ff990) at ./nptl/futex-internal.c:57
* 2    Thread 0x7ffff77ff6c0 (LWP 107977) "simple" hello () at simple.cpp:6
```

The thread was spanned in the statement `std::thread t1 {hello};`
and was joined in the statement `t1.join();`

### References

- Anthony Williams, C++ Concurrency in Action, 2nd Edition, Manning Publications.

