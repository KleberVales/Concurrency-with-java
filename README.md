# Concurrency-with-java

## Introducing Threads
### Comparing to Virtual Threads
### Understanding Thread Concurrency
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

A daemon thread is one that will not prevent the JVM from exiting when the program finishes.

Let’s take a look at an example. What do you think this outputs?

```java

public class Zoo {
    public static void pause() { // Defines the thread task
        try {
            Thread.sleep(10_000); // Wait for 10 seconds
        } catch (InterruptedException e) {
            System.out.println(“Thread finished !”);
        }
        
    }

    public static void main(String[] unused) {
        var job = Thread.ofPlatform().start(Zoo::pause);
        System.out.println(“Main method finished !”);
    }
}

```

```bash

Main method finished!
< 10 second wait >
Thread finished!

```
Change for deamon
```java
     var job = Thread.ofPlatform().daemon(true).start(Zoo::pause);
```


### Managing a Thread’s Life Cycle

<img width="981" height="541" alt="Captura de tela 2025-11-11 143554" src="https://github.com/user-attachments/assets/62f8e543-a6c1-484a-8556-fc6f1b236345" />


## Creating Threads with the Concurrency API

The Concurrency API includes the ExecutorService interface, which defines services that create and manage threads.

### Introducing the Single-Thread Executor

Since ExecutorService is an interface, how do you obtain an instance of it? The Concurrency API includes the Executors factory class that can be used to create instances of the ExecutorService object.

```java

try (ExecutorService service = Executors.newSingleThreadExecutor()) {
      System.out.println("begin");
      service.execute(printInventory);
      service.execute(printRecords);
      service.execute(printInventory);
      System.out.println("end");
}

```

### Submitting Tasks

You can submit tasks to an ExecutorService instance multiple ways.

shows the five methods, including execute() and two submit() methods, that you should know for the exam.

| Method Name | Description |
|-------------|-------------|
| `void execute(Runnable command)` | Executes Runnable task at some point in future. |
| `Future<?> submit(Runnable task)` | Executes Runnable task at some point in future and returns Future representing task. |
| `<T> Future<T> submit(Callable<T> task)` | Executes Callable task at some point in future and returns Future representing pending results of task. |
| `<T> List<Future<T>> invokeAll(Collection<? extends Callable<T>> tasks)` | Executes given tasks and waits for all tasks to complete. Returns List of Future instances in the same order in which they were in original collection. |
| `<T> T invokeAny(Collection<? extends Callable<T>> tasks)` | Executes given tasks and waits for at least one to complete. |

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

### Combining Results with collect()

### Performing a Parallel Reduction on a Collector









