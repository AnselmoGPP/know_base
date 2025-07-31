# Multithreading

## Table of Contents
+ [Introduction](#introduction)
+ [Managing threads](#managing-threads)
+ [Sharing data between threads](#sharing-data-between-threads)
+ [Synchronizing concurrent operations](#synchronizing-concurrent-operations)
+ [The cpp memory model and operations on atomic types](#the-cpp-memory-model-and-operations-on-atomic-types)
+ [Designing lock-based concurrent data structures](#designing-lock-based-concurrent-data-structures)
+ [Designing lock-free concurrent data structures](#designing-lock-free-concurrent-data-structures)
+ [Designing concurrent code](#designing-concurrent-code)
+ [Advanced thread management](#advanced-thread-management)
+ [Testing and debugging multithreaded applications](#testing-and-debugging-multithreaded-applications)


## Resources

- Anthony Williams (2012) _**C++ concurrency in action**_. Manning. Shelter island. Retrieved from [here](https://www.bogotobogo.com/cplusplus/files/CplusplusConcurrencyInAction_PracticalMultithreading.pdf).
- Ari Saif (2018) _**Multithreading in 5 minutes**_. hackernoon. Retrieved from [here](https://hackernoon.com/learn-c-multi-threading-in-5-minutes-8b881c92941f).
- Deb Haldar (2017) _**Top 20 multithreading mistakes**_. acodersjourney. Retrieved from [here](https://acodersjourney.com/top-20-cplusplus-multithreading-mistakes/).


## Introduction

### What is concurrency?

C++11 supports multithreaded programs without relying on platform-specific extensions.

**Concurrency**: Two or more activities happening at the same time. In computer systems, it’s a single system performing multiple independent activities in parallel, rather than sequentially.

**Task switching**: One processor can only perform one task at a time, but can switch between tasks many time per second, giving the illusion of some tasks happening concurrently. To do the interleaving between threads, it performs a **context switch**.

**Hardware concurrency**: Multiple processors or multiple cores within a processor (or both) can genuinely run more than one task in parallel.

**Two basic approaches** to concurrency (you can combine both):

- **Multiple single-threaded processes**:

  - Communication between them is complicated to set up or slow or both because the OS usually protects processes to avoid one process accidentally modifying data belonging to another process.
  - Overhead
  - Easier to write safe concurrent code with processes rather than threads.
  - C++ Standard doesn’t provide any intrinsic support for communication between processes, so these applications have to rely on platform-specific APIs to do so.

- **Multiple threads in a single process**:

  - Each thread runs independently of the others, but most of the data can be accessed directly from all threads. Sharing memory among processes is complicated to set up and often hard to manage.
  - Low overhead (because of shared address and lack of protection of data).
  - If data is accessed by multiple threads, the programmer must ensure that the view of data seen by each thread is consistent whenever it’s accessed.
  - Favored approach to concurrency in mainstream languages.

### Why use concurrency?

- **Separation of concerns**:

  - Make programs easier to understand and test.
  - A DVD player app with input buttons (pause, return, quit…), in a single thread, would have to check for user input at regular intervals during playback.
  - Often used for running tasks that must run continuously in the background.
  - Here, the number of threads is independent of the number of CPU cores available.

- **Performance**:

  - The increased computing power of machines comes, not from running a single task faster, but from running multiple tasks in parallel.
  - Two ways of using concurrency for performance.
    - **Task parallelism**: Divide a single task into parts and run each in parallel. It may be a complex process if there are many dependencies.
      - **Processing parallelism**
      - **Data parallelism**
    - **Used to solve bigger problems**: It takes the same amount of time to process one chunk of data, but more data can be processed in the same amount of time.

**When not to use concurrency?**

When the benefit is not worth the cost. Code using concurrency is harder to understand. Unless the potential performance gain is large enough or separation of concerns clear enough to justify the additional development time required to get it right and the additional costs associated with maintaining multithreaded code, don’t use concurrency.

Performance gain might not be as large as expected; there’s an inherent overhead associated.

Threads are a limited resource. It consumes OS resources and make the whole system run slower. Each process requires a separate stack space, so available memory or address space for a process. Thread pools may limit the number of threads.

The more threads you have, the more context switching the OS has to do. Each context switch takes time, and at some point adding an extra thread will reduce the performance.

Concurrency complicates the code, making it harder to understand and more prone to bugs.

### Concurrency and multithreading in C++

**Efficiency in the C++ Thread Library**:

**Abstraction penalty**: Implementation costs associated with using any high-level facilities, compared to using the underlying low-level facilities directly.

The C++ SL is designed in a way that there should be little or no benefit to be gained from using the lower-level APIs directly.

- Thus, the C++ Thread Library provides an efficient implementation, with very low abstraction penalty, on most platforms.
- It provides sufficient low-level facilities for those wishing to work close to the metal for the ultimate performance: Along with the new memory model comes a comprehensive atomic operations library for direct control over individual bits and bytes and the inter-thread synchronization and visibility of any changes.
- It provides higher-level abstractions and facilities that make writing multithreaded code easier and less error prone, though sometimes they may come with a performance cost. However, this cost doesn't necessarily imply a higher abstraction penalty because writing the abstraction yourself generally won't reduce such cost, and the compiler may inline much of the additional code.
- High-level facilities may provide additional functionality beyond what you require. But most of the time this is not an issue: you don’t pay for what you don’t use.
- Handcrafting the desired functionality from lower-level facilities may produce more complex and error prone code, while improving your application's design can offer much more performance gains.

In those very rare cases where the SL does not provide the required performance or behaviour, it might be necessary to use platform-specific facilities.

**Platform-specific facilities**:

On any given platform there will be platform-specific facilites that go beyond what’s offered by C++ Standard. To gain access to those facilities without giving up the benefits of Standard C++ Thread library, the types in the C++ Thread library may offer a `native_handle()` member function that allows the underlying implementation to be directly manipulated using a platform-specific API. Any operatios performed using native_handle()  are entirely platform dependent.

### Getting started

The only real distinction between a multi-threaded program and single-threaded program is that some functions might be running concurrently, so you need to ensure that shared data is safe for concurrent access.

Functions and classes for managing threads are declared in `<thread>`, whereas those for protecting shared data are in other headers.

Every thread has to have an initial function (where the new thread of execution begins). The initial thread in an application is main().

`join()` causes the calling thread to wait for the thread associated with the std::thread object.


## Managing threads

### Basic thread management

Every C++ program has at least one thread (`main()`). Your program can then launch additional threads that have another function as the entry point. When the specified entry point function returns, the thread exits. Threads are started by constructing a std::thread object that specifies the task to run on that thread.

**Callable object**: Something that can be called like a function, with the syntax `object()` or `object(args)`; that is, a function pointer or an object of a class type that overloads operator(). The overload of `operator()` in your class makes it callable.

`std::thread` also works with any callable type, so you can pass an instance of a class with a **function call operator**.

```
class task {
public:
    void operator() () const {
        do_something();
    }
};

task obj;
std::thread myThread(obj);
```

The supplied function object is copied into the storage belonging to the newly created thread of execution and invoked from there.

If you pass a **temporary** rather than a named variable, then the syntax can be the same as that of a function declaration, in which case the compiler interprets it as such, rather than an object definition.

```
std::thread myThread(task());
```

This declares a function `myThread()` that takes a single parameter (a pointer to a function taking no parameters and returning a task object) and returns a `std::thread` object, rather than launching a new thread. Avoid this by naming your function object by using an extra set of parentheses, or by using the new uniform initialization syntax.

```
std::thread myThread((task()));
```

```
std::thread myThread{task()};
```

One type of callable object that avoids this problem is a **lamba expression**.

```
std::thread myThread( [] {
    do_something();
});
```

Once you’ve started your thread, you need to explicitly decide whether to wait for it to finish (by **joining**) or leave it to run on its own (by **detaching**). If you don’t decide before the std::thread object is destroyed, then your program is terminated (std::thread destructor calls **`std::terminate()`**).

Ensure that the data accessed by the thread is valid until the thread has finished with it. Example: The thread function holds pointers or references to local variables and the thread hasn’t finished when the function exits. Avoid this by making the thread function self-contained (copy the data into the thread rather than sharing the data), or ensure that the thread has completed execution before the function exits by joining with the thread.

`join()`: Call it on the associated std::thread instance for waiting for a thread to complete. It also cleans up any storage associated with the thread, so the `std::thread` object is no longer associated with the now-finished thread; it isn’t associated with any thread. This means that you can call `join()` only once for a given thread; once you’ve called `join()`, the std::thread object is no longer joinable, and `joinable()` will return false.

**Waiting in exceptional circumstances**: You need to ensure that you’ve called either `join()` or `detach()` before a `std::thread` object is destroyed. The call to `join()` is liable to be skipped if an exception is thrown after the thread has been started but before the call to `join()`. In general, if you were intending to call `join()` in the non-exceptional case, you also need to call `join()` in the presence of an exception to avoid accidental lifetime problems.

You can use a **try/catch block** but it’s verbose and it’s easy to get the scope slightly wrong. Another way is to use the standard **RAII** (Resource Acquisition Is Initialization) idiom and provide a class that does the `join()` in its destructor.

**Running threads in the background**: Calling `detach()` on a `std::thread` object leaves the thread to run in the background, with no direct means of communicating with it. This breaks the association of the thread with the `std::thread` object and ensures that `std::terminate()` won’t be called when the `std::thread` object is destroyed. It can no longer be joined. Ownership and control are passed over to the C++ Runtime Library. Such threads are typically long-running (example: word processor that can edit multiple documents at once).

### Passing arguments to a thread function

Passing arguments to the callable object or function is as simple as passing additional arguments to the std::thread constructor.

By default, arguments are **copied** into internal storage (even when parameters expect a reference).

When a reference is expected, the std::thread constructor only copies the supplied values, so it will end up passing a reference to an internal copy of that argument and not a reference to the original argument variable itself. Any modifications made on this argument will not affect the original argument and will be discarded when the thread ends (the copied values are destroyed).

```
void f(int i, std::string const & s);
std::thread t(f, 5, "hello");
```

The string literal is passed as a char const* and converted to a std::string only in the context of the new thread.

```
void f(int i, std::string const & s);
void wrong() {
    char buffer[10000];
    std::thread t(f, 5, buffer);
    t.detach();
}
```

It’s very possible that the function `wrong()` will exit before the buffer variable has been converted to a std::string on the new thread, resulting in undefined behaviour. Solution: **cast** to std::string before passing the buffer.

```
std::thread t(f, 5, std::string(buffer));
```

To pass a reference, and not a copy, you can wrap the arguments that really need to be references in **`std::ref`**.

```
void funct(int i, widget& data);
std::thread f(f, 5, std::ref(data));
```

You can pass a **member function pointer** as the function, provided you supply a suitable object pointer as the first argument. You can also supply arguments to it.

```
class myClass {
public:
    void work();
};

myClass obj;
std::thread t(&myClass::work(), &obj);     // this invokes obj.work()
```

The third argument, and so forth, to the std::thread constructor will be the arguments.

Another scenario: **Data held within one object is transferred** over to another, leaving the original object “empty”. Example:

**`std::unique_ptr`**: Provides automatic memory management for dynamically allocated objects. Only one std::unique_ptr instance can point to a given object at a time, and when that instance is destroyed, the pointer-to object is deleted. The move constructor and move assignment operator allow the ownership of an object to be transferred around between std::unique_ptr instances. Such transfer leaves the source object with a NULL pointer. This moving of values allows objects of this type to be accepted as function parameters or returned from functions. Where the source object is a temporary, the move is automatic, but where the source is a named value, the transfer must be requested directly by invoking std::move().

```
void process_big_object(std::unique_ptr<big_object>);
std::unique_ptr<big_object> p(new big_object);
p->prepare_data(42);
std::thread t(process_big_object, std::move(p));
```

By specifying std::move(p) in the std::thread constructor, the ownership of the big_object is transferred first into internal storage for the newly created thread and then into process_big_object.

### Tranferring ownership of a thread

48













## Sharing data between threads

## Synchronizing concurrent operations

## The cpp memory model and operations on atomic types

## Designing lock-based concurrent data structures

## Designing lock-free concurrent data structures

## Designing concurrent code

## Advanced thread management

## Testing and debugging multithreaded applications

