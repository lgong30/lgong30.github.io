---
layout: post
title: Running Time Measurement (C++)
tags: [C++]
categories: [skill]
---

Running time measurement is very important when you want to know the empirical time complexity of your "algorithm" or when you want to provide some progress status of your running program (for example, how long will 
your program continue before finish a specific task). In MATLAB, you can use `tik tok`; in Python, you can use `timeit` or `time` package; What about in C++. In this post, we will give a few macros for you to conduct the time 
measurement task.



Run Time Measurement Macros for C++
-----------------------------------

```cpp
#include <chrono>  
#define TIMING  

#ifdef TIMING  
#define INIT_TIMER auto start = std::chrono::high_resolution_clock::now();  
#define START_TIMER  start = std::chrono::high_resolution_clock::now();  
#define STOP_TIMER(name)  std::cout << "RUNTIME of " << name << ": " << \  
    std::chrono::duration_cast<std::chrono::milliseconds>( \
            std::chrono::high_resolution_clock::now()-start \
    ).count() << " ms " << std::endl; 
#else  
#define INIT_TIMER  
#define START_TIMER  
#define STOP_TIMER(name)  
#endif  
```

Please make sure that your compiler support `C++11`, and you do use `C++11` or higher to compile your code. For example, if you want to compile your C++ code with C++11 by using g++, you can simply add the following flag: `-std=c++11`


An Example
----------

The following presents a simple example, which uses the above macros to measure running time (it assumes that the above macros are defined in `tm.h`).

```cpp
#include <iostream>
#include "tm.h"

inline int add(int a, int b) {
    return a + b;
}

int main()
{
    // initialize a timer
    INIT_TIMER
    
    int repeat_times = 10000000;
    // start the time
    START_TIMER
    for (int i = 0;i < repeat_times;++ i) {
        add(100, 10);
    }
    // stop the timer and printing out the time information
    STOP_TIMER("adding two integers for repeating " + std::to_string(repeat_times) + " times")

    return 0;

}
```

If you run the above code correctly, you should see an output similar like below:

```shell
$ RUNTIME of adding two integers for repeating 10000000 times: 19 ms
``` 


