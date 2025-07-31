# Generic algorithms

## Table of Contents
+ [Overview](#overview)
+ [Customizing operations](#customizing-operations)
+ [Revisiting iterators](#revisiting-iterators)
+ [Structure of generic algorithms](#structure-of-generic-algorithms)
+ [Container-specific algorithms](#container-specific algorithms)


## Overview

### Basics

**Generic algorithms**: Algorithms that operate on different types of containers (container-independent) and on elements of various types. In general, they don't work directly on a container, but by traversing a range of elements bounded by two iterators. They never execute container operations. The library (`<algorithm>` and `<numeric>`) provides more than 100 algorithms but, like containers, they have a consistent architecture. Most of them operate over a range of elements (input range) denoted by their first two parameters (iterators to the first and one past the last elements to process). 

Example: `std::find(iter1, iter2, val)`

```
auto result = find(vec.cbegin(), vec.cend(), 42);
```

```
auto result = find(list.cbegin(), list.cend(), "myValue");
```

```
int ia[] = { 25, 38, 74, 69, 17, 76 };
int* result_1 = find(begin(ia), end(ia), 38);
auto result_2 = find(ia + 1, ia + 4, 69);
```

**Algorithms dependencies**:

- **Container independent**: Iteration through the elements is handled by iterator operations. This implies that they never change container's size (it may change values of elements and move them around, but never add or remove elements directly). 
- **Element-type dependent**: Most of them use operations of the element type. However, most algorithms provide a way for us to supply our own operation to use in place of the default operator.

**Inserters** are a special class of iterators that can also execute insert operations on the underlying container. When an algorithm operates on one of them, the inserter can add elements, but the algorithm itself never does so.

### Read-only algorithms

They read, but never write, to the elements in their input range. Examples:

- `**find**(it1, it2, val)`: Uses `==` operator. Find an element in the input range.
- `**accumulate**(it1, it2, initialVal)`: Uses `+` operator. Add up all the elements in the input range. 
  - Note: Since strigs have `+` operator, this would concatenate the elements of a `vector<string>` (`accumulate(a, b, string("")`). Passing a string literal (`const char*`) as third parameter would be a compile-time error because it has no `+` operator.
- `**equal**(it1, it2, it3)`: Uses `==`. Check if two sequences are equal. It assumes that both sequences have same length (). The element types of both sequences need not be the same as long as we can use `==` to compare the elements (like `vector<string>` and `list<const char*>`).

It's good practice to use `cbegin()` and `cend()` with read-only algorithms, unless you plan to use the returned iterator to change the element's value.

### Write algorithms

They can assign new values to the elements in their input range. We must ensure that the sequence is at least as large as the number of elements we ask the algorithm to write.






## Customizing operations
## Revisiting iterators
## Structure of generic algorithms
## Container-specific algorithms

