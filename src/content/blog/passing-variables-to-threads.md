---
title: Passing Variables to a Thread
description: Learn how to pass variables and data to threads in C++
pubDate: 2026-07-17
heroImage: '../../assets/threads.png'
---

## Overview

When working with threads, a common requirement is passing data or variables to the thread function. 
This guide covers the various methods and best practices for passing variables to threads in C++.

## Basic Thread Creation with Arguments

Arguments are first copied into the thread objects internal storage,
and then passed to the callable object or function as rvalues as if they were temporaries.

```cpp
#include <iostream>
#include <thread>

class Test
{
public:
    Test() { std::cout << "Default constructor\n"; }

    Test(const Test&)
    {
        std::cout << "Copy constructor\n";
    }

    Test(Test&&)
    {
        std::cout << "Move constructor\n";
    }
};

void worker(Test t)
{
    std::cout << "Worker running\n";
}

int main()
{
    Test obj;
    std::thread t(worker, obj);
    t.join();
}
```
The two stages can be seen in the following output. 
Copy followed by moving.

```bash
$ ./thread_argument_storage 
Default constructor
Copy constructor
Move constructor
Worker running
```

Now lets see the case when we pass a rvalue to the thread's object creation.
Note that `std::move` casts a lvalue to a rvalue.

```cpp
int main()
{
    Test obj;
    std::thread t(worker, std::move(obj));
    t.join();
}
```

```bash
$ ./thread_argument_storage 
Default constructor
Move constructor
Move constructor
Worker running
```


### References

- Anthony Williams, C++ Concurrency in Action, 2nd Edition, Manning Publications.
