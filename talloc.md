---
layout: default
title: Talloc 
permalink: /talloc/
---
Current version: 1.4.0

## About 

{: style="text-align: justify;"}
Custom thread-safe malloc implementation with pooling of small objects (~2KB) and fast AVL tree based best-fit memory 
allocation written in C. Source code can be found [here](https://github.com/travisdoor/talloc).

{: style="text-align: justify;"}
Talloc operates in preallocated memory block reserved on startup and returned back to the system on application 
shutdown. Due to preallocation, talloc reduces calls to the system memory allocation. Objects smaller than 2KB (by default)
are sorted into groups and allocated in pools (each size has it's own pool). Talloc stores some meta data about
allocated blocks, this leads to higher memory consumption it is designed for better speed not less memory usage.
It is successfully used by the Sandy Engine in Planet Nomads and also each of my personal projects uses this allocator.

## Change log
  * 1.4.0 Add exception method setter. 
  * 1.3.0 Add exception handling and checking for invalid pointer freeing.
  * 1.2.0 Locking in pool and MSVC support.
  * 1.1.1 Fix aba problem random crashes in multithread pool access.
  * 1.1.0 Add talloc_force_reset method.
  * 1.0.1 Add documentation and minor bug fixes.
  * 1.0.0 Initial version.

## How to use
### Building 
#### Supported compilers
  * GCC
  * clang
  * MinGW
  * MSVC

#### MacOS or Linux
Build the project with cmake.

{% highlight bash %}
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=Release ..
make
{% endhighlight %}

#### Windows
Build talloc on windows with MinGW using cmake.

{% highlight bash %}
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=Release .. -G"MinGW Makefiles"
cmake --build . --config Release
{% endhighlight %}

To use the dll with MSVC you must create lib file first with lib.exe utility. 
[Guide here.](http://www.mingw.org/wiki/MSVC_and_MinGW_DLLs)

Build talloc on windows with MSVC using cmake.

{% highlight bash %}
mkdir build
cd build
cmake .. -G"Visual Studio 15 Win64"
cmake --build . --config Release
{% endhighlight %}

### Linking
Link libtalloc library and include include/talloc.h interface.

### Usage

{% highlight c %}
#include "talloc.h"

// allocation
foo_t *foo = (foo_t *)tmalloc(sizeof(foo_t));
// some useful stuff
tfree(foo);
foo = NULL;
{% endhighlight %}

## Notes 

{: style="text-align: justify;"}
Preallocated memory will never be returned to the system automatically, you can use talloc_force_reset method 
(can be enabled in config.h) to free system memory and reset allocator to initial state (make sure that already allocated
memory will never be used after the reset method call). The memory will be returned back to the system on application exit 
on most platforms.

