# Chapter 5. The C++ memory model and operations on atomic types

## 5.1. Memory model basics

### 5.1.1. Objects and memory locations

All data in a C++ program is made up of objects.

The C++ Standard defines an object as “a region of storage,” although it goes on to assign properties to these objects, such as their type and lifetime.

There are four important things to take away from this:
- Every variable is an object, including those that are members of other objects.
- Every object occupies at least one memory location.
- Variables of fundamental types such as int or char occupy exactly one memory location, whatever their size, even if they’re adjacent or part of an array.
- Adjacent bit fields are part of the same memory location.

### 5.1.2. Objects, memory locations, and concurrency

In order to avoid the race condition, there has to be an enforced ordering between the accesses in the two threads.

One way to ensure there’s a defined ordering is to use mutexes; if the same mutex is locked prior to both accesses, only one thread can access the memory location at a time, so one must happen before the other.

The other way is to use the synchronization properties of atomic operations either on the same or other memory locations to enforce an ordering between the accesses in the two threads.

### 5.1.3. Modification orders

Every object in a C++ program has a modification order composed of all the writes to that object from all threads in the program, starting with the object’s initialization. In most cases this order will vary between runs, but in any given execution of the program all threads in the system must agree on the order.

Although all threads must agree on the modification orders of each individual object in a program, they don’t necessarily have to agree on the relative order of operations on separate objects.

## 5.2. Atomic operations and types in C++

An atomic operation is an indivisible operation. You can’t observe such an operation half-done from any thread in the system; it’s either done or not done.

### 5.2.1. The standard atomic types

The standard atomic types can be found in the <atomic> header.

In fact, the standard atomic types themselves might use such emulation: they (almost) all have an is_lock_free() member function, which allows the user to determine whether operations on a given type are done directly with atomic instructions (x.is_lock_free() returns true) or done by using a lock internal to the compiler and library (x.is_lock_free() returns false).

This is important to know in many cases—the key use case for atomic operations is as a replacement for an operation that would otherwise use a mutex for synchronization; if the atomic operations themselves use an internal mutex then the hoped-for performance gains will probably not materialize, and you might be better off using the easier-to-get-right mutex-based implementation instead.

Since C++17, all atomic types have a static constexpr member variable, X::is_always_lock_free, which is true if and only if the atomic type X is lock-free for all supported hardware that the output of the current compilation might run on.

The macros evaluate to the value 0 if the atomic type is never lock-free, to the value 2 if the atomic type is always lock-free, and to the value 1 if the lock-free status of the corresponding atomic type is a runtime property

The only type that doesn’t provide an is_lock_free() member function is std::atomic_flag. This type is a simple Boolean flag, and operations on this type are required to be lock-free.

The standard atomic types are not copyable or assignable in the conventional sense, in that they have no copy constructors or copy assignment operators.

Each of the operations on the atomic types has an optional memory-ordering argument which is one of the values of the std::memory_order enumeration.

The permitted values for the memory ordering depend on the operation category. The operations are divided into three categories:
- Store operations, which can have memory_order_relaxed, memory_order_release, or memory_order_seq_cst ordering
- Load operations, which can have memory_order_relaxed, memory_order_consume, memory_order_acquire, or memory_order_seq_cst ordering
- Read-modify-write operations, which can have memory_order_relaxed, memory_order_consume, memory_order_acquire, memory_order_release, memory_order_acq_rel, or memory_order_seq_cst ordering

### 5.2.2. Operations on std::atomic_flag 
