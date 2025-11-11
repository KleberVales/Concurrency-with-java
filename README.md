# Concurrency-with-java

## Introducing Threads

- A thread is the smallest unit of execution that can be scheduled by the operating system.
- A process is a group of associated threads that execute in the same shared environment.
- It follows, then, that a single- threaded process is one that contains exactly one thread, whereas a multithreaded process contains one or more threads.
- By shared environment, we mean that the threads in the same process share the same memory space and can communicate directly with one another.
- A task is a single unit of work performed by a thread. A thread can complete multiple independent tasks but only one task at a time.

### Comparing to Virtual Threads

Platform threads are often inefficient. They are like having a personal butler who stands around in case you need something. If you constantly need things, this is a good use of the butler’s time. For a platform thread to be efficient, you need to be heavily using the CPU. 

By contrast, when we go to a restaurant, there is a server who is assigned to many tables. Since we don’t need someone to stand there while the food is cooking and when we eat, this is a more efficient use of the server’s time. The Java equivalent of a single server handling multiple tables is a carrier thread. The tables correspond to virtual threads, which are less resource intensive than platform threads, making virtual threads a good choice when you expect to wait for I/O or network resources.

### Understanding Thread Concurrency

The property of executing multiple threads and processes at the same time is referred to as concurrency. A thread scheduler determines which threads should be currently executing. For example, a thread scheduler may employ a round-robin schedule in which each available thread receives an equal number of CPU cycles with which to execute, with threads visited in a circular order.
