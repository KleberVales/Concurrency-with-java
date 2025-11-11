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

A thread scheduler may employ a round-robin schedule in which each available thread receives an equal number of CPU cycles with which to execute, with threads visited in a circular order.

When a thread’s allotted time is complete but the thread has not finished processing, a context switch occurs. A context switch is the process of storing a thread’s current state and later restoring the state of the thread to continue execution. Since there’s a cost to context switch due to lost time and having to reload a thread’s state, intelligent thread schedulers do their best to minimize the number of context switches while keeping an application running smoothly.

Finally, a thread can interrupt or supersede another thread if it has a higher thread priority. A thread priority is a numeric value associated with a thread that the thread scheduler considers when determining which threads should execute. The priority can be set from 1 (Thread.MIN_PRIORITY) to 10 (Thread.MAX_PRIORITY), either before a thread is started or while it is running.

```java

var thread1 = new Thread(() -> System.out.print("Super Important"));
thread1.setPriority(Thread.MAX_PRIORITY);
thread1.start();

```

```java

var thread2 = new Thread(() -> System.out.print("Less Important"));
thread2.start();
thread2.setPriority(2);

```

### Creating a Thread

- Runnable interface

```java

@FunctionalInterface
public interface Runnable {
     void run();
}

```

```java

Thread.ofPlatform().start(() -> System.out.print("Hello"));
System.out.print("World");

```

Creating and starting a Thread
| Code | Type | Description |
|------|------|-------------|
| `var builder = Thread.ofPlatform();`<br>`Thread thread = builder.start(runnable);` | Platform | Factory |
| `var builder = Thread.ofVirtual();`<br>`Thread thread = builder.start(runnable);` | Virtual | Factory |
| `Thread thread = new Thread(runnable);`<br>`thread.start();` | Platform | Constructor |

### Working with Daemon Threads

### Managing a Thread’s Life Cycle

## Creating Threads with the Concurrency API

### Introducing the Single-Thread Executor

### Submitting Tasks

### Waiting for Results

### Investigating Callable

### Shutting Down a Thread Executor

### Scheduling Tasks

### Increasing Concurrency with Pools

## Writing Thread-Safe Code

### Understanding Thread-Safety

### Protecting Data with Atomic Classes

### Improving Access with synchronized Blocks

### Understanding the Lock Framework

### Orchestrating Tasks with a CyclicBarrier

## Using Concurrent Collections

### Understanding Memory Consistency Errors

### Working with Concurrent Classes

### Obtaining Synchronized Collections

## Identifying Threading Problems

### Understanding Liveness

### Deadlock

### Starvation

### Livelock

### Managing Race Conditions

## Working with Parallel Streams

### Creating Parallel Streams

### Performing a Parallel Decomposition

### Processing Parallel Reductions

### Performing Order-Based Tasks

### Combining Results with reduce()









