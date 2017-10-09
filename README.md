# Memory Management Notes

## Problem: It's All About Lifetime

1. Object often outlives function.
2. Two ways to solve this problem in the sence of C programming language:
  - On the stack: Caller has automatic variable and send its storage to the callee. When the caller function exits, the storage is automatically destoryed by the C runtime.
    - (Add an example.)
    - Guaranteed memory safety, but difficult to design a beautiful API. More than often I need to escalate a shared object.
  - On the heap: independent from program but requires exclicit `free()`ing unused segments.
    - Unsafe.
    - More fitting to a recursive data structure (such as a linked-list).

## Unix Ways: `brk()` & `sbrk()`

1. The [process layout](https://notes.shichao.io/tlpi/ch7/) shows how `brk()` & `sbrk()` add storage to current program space. `brk()` works on addresss; `sbrk()` works on increment or decrement amounts.
2. `malloc()` is an libc supplied wrapper for `sbrk()` & `mmap()` depending on the allocation size (usually 128KB).
3. Checkouting the code of musl-libc, I find that it uses -1 as the "fildes" parameter when used as `malloc()`.

## Standard C: `malloc()` & `free()`

## Garbage Collection

1. Introducted (invent?) by John McCarthy in 1959 to ease memory management for LISP.

## libgc

1. Said to be conservative but don't know why.
2. An in-place replacement for `malloc()`.
3. Uses preemptive scheduling to do Mark-n-Sweep.
4. Can use another thread for GC.

## Useful links

1. [Shichao's Notes](https://notes.shichao.io/tlpi/ch7/)
2. [libgc](http://www.hboehm.info/gc/)
3. [利用 libgc 當作 malloc() 的漏偵測器](http://blog.csdn.net/freedom2028/article/details/4383838)
4. [GC myths](www.hboehm.info/gc/myths.ps)
5. [Paul Wilson's garbage collection ftp archive](ftp://ftp.cs.utexas.edu/pub/garbage/)
6. [GC survey](ftp://ftp.cs.utexas.edu/pub/garbage/gcsurvey.ps)
7. [GC FAQ -- draft](http://www.iecc.com/gclist/GC-faq.html)
