# Sequential containers

## Table of Contents
+ [Overview](#overview)
+ [Operations](#operations)
+ [How a vector grows](#how-a-vector-grows)
+ [Additional string operations](#additional-string-operations)
+ [Container adaptors](#container-adaptors)


## Overview

**Container**: Holds a collection of objects of a specified type.

**Sequential containers** hold elements whose position corresponds to the positions in which the elements are added to the container. They share a common interface, which each of the containers extends in its own ways. The library provides 3 **adaptors** that define a different interface to the container operations.

**Pros and cons**:

- **Pros**:
  - Fast sequential access to their elements
- **Cons**:
  - Slow to add/delete its elements
  - Slow to perform non-sequential access to its elements

**Types of sequential containers**

- **Non-linked lists**: Contiguous memory allocation. Efficient and flexible memory management. Fast random access (O(1)). Slow insertion/deletion (O(n)) (elements must be moved to maintain contiguity), except at the end.

  - **`std::array`**: Fixed-size array. Size fixed at compile-time, like C-style arrays. Safer and easier-to-use alternative to built-in arrays.
    - Fast random access
    - Cannot add or remove elements
    - Contiguous elements
  - **`std::vector`**: Flexible-size array. 
    - Fast random access
    - Fast insert/delete at the back
    - Contiguous elements in memory
  - **`std::deque`**: Double-ended queue.
    - Fast random access
    - Fast insert/delete at front or back
    - No contiguous elements
  - **`std::string`**: Similar to vector, but containing characters.
    - Fast random access
    - Fast insert/delete at the back
  - **Adaptors**: Container wrappers that provide a restricted interface.
    - `std::stack`: LIFO stack. Wraps `std::deque` by default (alternatives: `std::vector`, `std::list`).
    - `std::queue`: FIFO queue. Wraps `std::deque` by default (alternative: `std::list`).
    - `std::priority_queue`: Max-heap queue by default (alternative: min-heap). Wraps `std::vector` by default (alternative: `std::deque`). Elements are sorted based on priority (by default, largest value first). `push` inserts element while maintaining order. `pop` removes the highest-priority one. A max-heap is a binary tree, usually stored in an array, that keeps the largest element always at the top (a min-heap keeps the smallest).

- **Linked lists**: Dynamically allocated nodes linked together. Slow random access (O(n)). Fast insertion/deletion (O(1)).

  - **`std::list`**: Doubly-linked list.
    - Fast insert/delete at any point in the list (`std::list`)
    - No random access. Forward and reverse traversal.
    - More memory overhead than non-linked lists.
  - **`std::forward_list`**: Singly-linked list.
    - Fast insert/delete at the front.
    - No random access. Forward traversal.
    - More memory overhead than non-linked lists.

**Which container to use?** Rules of thumb depending on what your program needs:

- Ordinarily, it’s best to use **vector** unless there is a good reason to prefer another.
- Lots of small elements + space overhead matters: **non-linked-lists**.
  - Random access to elements: **vector** or **deque**.
  - Insert/delete elements at the front or back, but not in the middle: **deque**.
- Insert/delete elements in the middle of the container: **linked-lists**.
- Insert elements in the middle while reading input, but access randomly the rest of the time. Two options:
  - It’s often easier to append to a **vector** and then call **sort()**.
  - Use a **linked-list** for the input phase. After input, copy the list into a **vector**.
- Random access + insert/delete elements in the middle: It depends on the relative cost of accessing the elements in a **linked-list** versus inserting/deleting elements in a **vector/deque**. Generally, the predominant operation of the application determines the choice of container type (in such case, performance testing the application using both containers may be necessary).

If you’re not sure which container to use, write your code so that it uses only operations common to both std::vectors and std::lists: Use iterators, not subscripts, and avoid random access to elements. This way it will be easy to use either a vector or a list as necessary.

**forward_list** doesn’t have size() operation. For other containers, size() is guaranteed to be a fast, constant-time operation.

**std::arrays** have fixed size because the size is part of its type (like in a built-in array). We define an array specifying the element type and the container size (`array<int 10> myArray` = array containing 10 integers). If we list initialize it (`array<int, 5> = {1, 2, 3}`), the number of initializers must be equal to or less than the array’s size, and the rest of elements are value initialized (elements with class type must have default constructor to permit value initialization). We cannot copy or assign built-in array objects, but we can do it with std::arrays. When copying, the element type and size must be the same. We can copy built-in array types. Since its size is fixed, it doesn’t support `assign` nor assignment from a braced list.


## Operations

Excepting `arrays`, all library containers provide flexible memory management (its size can be changed dynamically at run time).

Below we can see many sequential container operations (other operations are common to only a smaller subset of the containers):

**Construction**

- `C c`: Default constructor where c is empty (unless C is array: the elements in c are default-initialized.
- __Copy entire objects__ (`C c1(c2)` or `C c1 = c2`): c1 is a copy of c2. Must have the same type. For array, must also have same size.
- `C c(b, e)`: Copy elements from the range denoted by iterators b and e. Type of elements must be compatible with the element type of C. Not valid for array.
- __List initialization__ (`C c{a, b, c...}` or `C c = {a, b, c...}`): c is a copy of the elements in the initializer list. Type of elements must be compatible with the element type of C. For array, the list must have same number or fewer than the size of the array (any missing elements are value-initialized).
- __Construct by size__: Constructors that take a size are only valid for sequential containers (except array).
  - `C seq(n)`: n value-initialized elements. This constructor is explicit. Not valid for strings. The element type has to be a built-in type or have default constructor (if it doesn’t have it, we must specify an explicit element initializer along with the size)
  - `C seq(n, t)`: n elements with value t.

**Assignment**: Assignment related operations invalidate iterators, references, and pointers into the left-hand container. They remain valid after a `swap` (aside from `string`) and the containers are swapped (excepting `arrays`).

- seq.assign(...): Replaces elements in `seq` with copies from elsewhere. Operations not valid for std::arrays.
  - `seq.assign(b, e)`: Replace with a range denoted by iterators (must not refer to `seq`). Destination and origin containers can be from different but compatible types.
  - `seq.assign({...})`: Replace with initializer list.
  - `seq.assign(n, t)`: Replace with n elements with value t.

```
list<string> names;
vector<const char*> oldstyle;
names = oldstyle;   // error
names.assign(oldstyle.cbegin(), oldstyle.cend());
```

**Adding elements**: Not supported by `array`. `forward_list` has a special version of `insert` and `emplace`. `push_back` and `emplace_back` are not valid for `forward_list`. `push_front` and `emplace_front` are not valid for `vector` or `string`. Adding elements to a `vector`, `string`, or `deque` may cause the entire object to reallocate, which invalidates all existing iterators, references, and pointers into the container.

- `c.push_back(t)`: Create element with value `t` at the end. Not valid for `forward_list`.
- `c.emplace_back(args)`: Construct element from `args` at the end.
- `c.push_front(t)`: Create element with value `t` at the front. Not valid for `vector` and `string`.
- `c.emplace_front(args)`: Construct element from `args` at the front.
- `c.insert(p, t)`: Create element with value `t` before element with iterator `p`. Returns iterator to new element.
- `c.emplace(p, args)`: Construct element from `args` before element with iterator `p`. Returns iterator to new element.
- `c.insert(p, n, t)`: Insert `n` elements with value `t` before element with iterator `p`. Returns iterator to first element inserted (or `p` if `n` == 0).
- `c.insert(p, b, e)`: Insert elements from iterator `b` to `e` before the element with iterator `p`. Returns iterator to first element inserted (or `p` if range is empty).
- `c.insert(p, il)`: Insert elements from a braced list of element values (`il`) before the element with iterator `p`. Return iterator to first element inserted (or `p` if list is empty).

**Accessing elements**: The access operations are undefined if the container has no elements.

- `c.back()`: Returns reference to last element. Undefined if empty. Not supported by `forward_list`.
- `c.front()`: Returns reference to first element. Undefined if empty.
- `c[n]`: Returns reference to element indexed. Undefined if `n >= c.size()`.
- `c.at(n)`: Returns reference to element indexed. Returns `out_of_range` exception if index is out of range. Provided by containers supporting random access.
- __Subscript operator ([])__: Returns reference to element indexed. Undefined if index is out of range. Provided by containers supporting random access.

**Erasing elements**: Not supported by `array`. `forward_list` has a special version of `erase`. Removing elements anywhere but the beginning or end of a `deque` invalidates all iterators, references, and pointers. Iterators, references, and pointers to elements after the erasure point in a `vector` or `string` are invalidated.

- `c.pop_back()`: Removes last element. Undefined if empty. Not valid for `forward_list`.
- `c.pop_front()`: Removes first element. Undefined if empty. Not valid for `vector` and `string`.
- `c.erase(p)`: Removes element with iterator p. Returns iterator to element after the one removed (or off-the-end iterator). Undefined if p is off-the-end iterator.
- `c.erase(b, e)`: Removes range of elements between 2 iterators. Returns iterator to element after the one removed (or off-the-end iterator).
- `c.clear()`: Removes all elements. Equivalent to `c.erase(c.begin(), c.end())`.

Adding or removing an element in a `forward_list` requires to know the element's predecessor, which is not easy here. Thus, it doesn't define `insert`, `emplace`, or `erase`. Instead, it defines other operations:

- `before_begin`: Iterator to the non-existent before-the-beginning element of the list.
- `cbefore_begin`: Like `before_begin` but returning a constant iterator.
- `insert_after`: Insert element/s after an iterator. Returns iterator to the last inserted element.
  - `insert_after(p, t)`: Insert object t after iterator p.
  - `insert_after(p, n, t)`: Insert n objects t after iterator p.
  - `insert_after(p, b, e)`: Insert a range of elements (between iterators b and e, not including e) after iterator p.
  - `insert_after(p, il)`: Insert a braced list after iterator p.
- `emplace_after(p  args)`: Construct an element after iterator p using args. Returns iterator to the new element. Undefined if p is off-the-end iterator.
- `erase_after`: Remove element/s after an iterator. Returns iterator to the element after the one deleted, or the off-the-end iterator.
  - `erase_after(p)`: Remove element after iterator p.
  - `erase_after(b, e)`: Remove range of elements (between iterators b and e, not including e).

**Resize** operation: It makes a container (except `array`s) larger or smaller. It means adding or deleting elements from the back of the container. If the container holds elements of a class type and resizing adds elements, we must supply an initializer or the element type must have a default constructor. Iterators, references, and pointers to deleted elements are invalidated. Resizing a `vector`, `string`, or `deque` potentially invalidates all iterators, pointers, and references.

- `resize(n)`: Resize to size n.
- `resize(n, t)`: Resize to size n. Any added element have value t.

**invalid pointers, references, and iterators**: Adding or removing elements from a container can invalidate pointers, references, or iterators to contained elements. Using them is a serious run-time error.

- After adding an element, iterators, pointers, and references…

  - … to a `vector` or `string` are invalid if the container is reallocated. If it's not, only those elements after the insertion are invalid.
  - … to a `deque` are invalid if we add elements anywhere but at the front or back. If we add at the front or back, iterators are invalidated, but references and pointers to existing elements are not.
  - … to a `list` or `forward_list` remain valid (including off-the-end and before-the-beginning iterators).

- After removing an element, all other iterators, pointers, and references…

  - … to a `vector` or `string` remain valid for elements before the removal point. The off-the-end iterator is always invalidated when we remove elements.
  - … to a `deque` are invalidated if the removed elements are not at the front or back. If it's at the back, only the off-the-end iterator is invalidated. If it's at the front, only the before-the-beginning iterator is invalidated. 
  - … to a `list` or `forward_list` remain valid (including off-the-end and before-the-beginning iterators).

Try to minimize the part of the program during which an iterators, reference, or pointer to a container element must stay valid. When adding or removing elements, ensure that the iterator is repositioned appropriately on each loop iteration, specially for `vector`, `string`, and `deque`. This is easy with `insert` and `erase` because they return iterators.

```
// Remove even-valued elements and duplicate each odd-valued one.
std::vector<int> v;
auto iter = v.begin();
while(iter != v.end())
  if(*iter % 2)
  {
    iter = v.insert(iter, *iter);
    iter += 2;
  }
  else
    iter = v.erase(iter);
```

Avoid storing the `end` iterator when iterating through loops that insert or delete elements (call `end()` instead). When we add or remove elements in a `vector` or `string`, or add elements or remove any but the first element in a `deque`, the `end` iterator is always invalidated.


## How a vector grows

 (`vector`, `string`, `deque`): To support fast random access, `vector` elements are stored contiguously. However, to add a new element, it would have to allocate new memory for the existing elements plus the new one, move the elements, and deallocate the old memory, which is inefficient. To reduce the number of reallocations, when `vector` or `string` have to get new memory they typically allocate **capacity** beyond what is immediately needed (implementation dependent) (for example, by doubling it). It holds this storage in reserve and uses it to allocate new elements as they're added. This technique improves performance so much that `vector` usually grows more efficiently than a `list` or `deque`. A `vector` must not allocate new memory until it's forced to do so. A `vector` is required to ensure that using `push_back` to add elements is efficient (i.e., the execution time of creating an n-element vector using push_back n times on an initially empty vector must never be more than a constant multiple of n). Container size management operations:

- `size()`: Number of elements the container holds.
- `c.capacity()`: Number of elements c can hold before reallocation is necessary.
- `resize(n)`: Changes `size` (number of elements stored), not `capacity`.
- `c.reserve(n)`: Changes `capacity`, not `size`. Allocates space for at least n elements. If requested size > current capacity, it allocates as much space or more; otherwise, it does nothing.
- `c.shrink_to_fit()`: Reduce `capacity()` to equal `size()`. However, the implementation is free to ignore this request.


## Additional string operations

- Construction:

  - `str(cp)`: Copy the array pointed by cp (`const char*`). Characters are copied up to the null, so the pointed array must be null terminated
  - `str(cp, n)`: Copy first n characters from the array pointed by cp (`const char*`).
  - `str(str2, pos)`: Copy string str2 starting at index pos.
  - `str(str2, pos, len)`: Copy len characters from string str2 starting at index pos. If pos is out of range, it throws out_of_range exception. If len > str.size(), it only copies up to str2 size.

- Substring: Returns a string that is a copy of part or all of the original string.

  - `s.substr(pos, n)`: Returns string of n characters starting at pos. n defaults to a value that causes the library to copy all characters in s starting from pos. Pos defaults to 0. If pos exceeds s size, it throws an out_of_range exception. If pos + n > s size, n is adjusted to copy only up to the end of s.

- Modifying strings:

  - `s.assign(args)`: Replace characters in s according to args. Returns reference to s.
  - `s.append(args)`: Appends args to s. Returns reference to s.
  - `s.erase(pos, len)`: Remove len characters starting at position pos. If len is omitted, removes characters from pos to the end of s. Returns reference to s.
  - `s.insert(pos, args)`: Insert characters specified by args before pos. Pos can be an index or iterator. Return value: if pos == index, returns reference to s; if pos == iterator, returns iterator to first inserted character.
  - `s.replace(range, args)`: Remove range of characters from s and replace them with the characters formed by args. Range can be an index and a length (`pos, len`), or a pair of iterators into s (`b, e`). Returns a reference to s. Replace is a shorthand of erase and insert.

Parameters meaning:

  - `args` has the following forms. `append` and `assign` can use all forms. `str` must be distinct from `s`. Iterators `b` and `e` may not refer to `s`.

    - `str`: String str.
    - `str, pos, len`: Up to len characters from str starting at pos.
    - `cp, len`: Up to len characters from the character array pointed to by cp.
    - `cp`: Null-terminated array pointed to by pointer cp.
    - `n, c`: n copies of character c.
    - `b, e`: Characters in the range formed by iterators b and e.
    - `initializer_list`: Comma-separated list of characters enclosed in braces.

  - `args` for `replace` and `insert` depend on how `range` or `pos` is specified:

    - `s.replace(pos, len, args)`: `args` can be `str`, `str, pos, len`, `cp, len`, `cp`, `n, c`.
    - `s.replace(b, e, args)`: `args` can be `str`, `cp, len`, `cp`, `n, c`, `b2, e2`, `initializer_list`.
    - `s.insert(pos, args)`: `args` can be `str`, `str, pos, len`, `cp, len`, `n, c`.
    - `s.insert(iter, args)`: `args` can be `n, c`, `b2, e2`, `initializer_list`.

- Search: The string class provides 6 different search methods, each one with 4 overloaded versions. They return the index of the character where the matched occurred (as `string::size_type`), or the static member `string::npos` if not found (unsigned value representing the largest possible string size).

  - `s.find(args)`: Find first occurrence of args in s.
  - `s.rfind(args)`: Find last occurrence of args in s.
  - `s.find_first_of(args)`: Find first occurrence of any character from args in s.
  - `s. find_last_of(args)`: Find last occurrence of any character from args in s.
  - `s.find_first_not_of(args)`: Find first character in s that is not in args.
  - `s.find_last_not_of(args)`: Find last character in s that is not in args.

`args` must be one of:

  - `c, pos`: Look for character c starting at position pos in s. Pos defaults to 0.
  - `s2, pos`: Look for string s2 starting at position pos in s. Pos defaults to 0.
  - `cp, pos`: Look for a C-style null-terminated string (pointed by pointer cp) starting at position pos in s. Pos defaults to 0.
  - `cp, pos, n`: Look for first n characters in an array (pointed by pointer cp) starting at position pos in s. No default for pos or n.

- Compare: There're 6 versions of the `compare` function. Like the C library `strcmp`, they return 0 or a positive or negative value depending on whether string s is equal to, greater than, or less than the string formed from the arguments.

  - `s.compare(args)`: Parameters `args` have different forms:

    - `s2`: Compare s to s2.
    - `pos1, n1, s2`: Compares n1 characters starting at pos1 from s to s2.
    - `pos1, n1, s2, pos2, n2`: Compares n1 characters starting at pos1 from s to the n2 characters starting at pos2 in s2.
    - `cp`: Compares s to the null-terminated array pointed to by cp.
    - `pos1, n1, cp`: Compares n1 characters starting at pos1 from s to cp.
    - `pos1, n1, cp, n2`: Compares n1 characters starting at pos1 from s to n2 characters starting from the pointer cp.

- Numeric conversions: In general, the character representation of a number differs from its numeric value (example: "0" has decimal value 48). Some functions can convert between numeric data and library strings.

  - `to_string(val)`: Overloaded function that returns the string representation of val, where val can be any arithmetic type.
  - stoX(s, p, b): Return the initial substring of s that has numeric content as an X type. The first non-whitespace character in the input string must be a character that can appear in a number. It reads this string until it finds a character that cannot be part of a number and converts the founded substring. The numeric base is b (10 by default), and p is a pointer to a size_t in which to put the index of the first nonnumeric character in s (0 by default, in which case it doesn't store the index). The first non-whitespace character in the string we convert to numeric value must be a sign (`+` or `-`), a digit (including `0x` or `0X` for hexadecimals). For conversions to floating-point, it may start with a decimal point `.` and contain an `e` or `E` for exponent. For conversions to integral types, depending on the base, it can contain alphabetic characters for numbers beyond 9. If the string cannot be converted to a number, it throws an `invalid_argument` exception. If the conversion cannot be represented, it throws `out_of_range`.
    - `stoi(s, p, b)`: To `int`
    - `stol(s, p, b)`: To `long`
    - `stoul(s, p, b)`: To `unsigned long`
    - `stoll(s, p, b)`: To `long long`
    - `stoull(s, p, b)`: To `unsigned long long`
    - `stof(s, p)`: To `float`
    - `stod(s, p)`: To `double`
    - `stold(s, p)`: To `long double`


## Container adaptors

**Adaptor**: Mechanism for making one thing act like another.

**Container adaptor**: Adaptor that takes an existing container type and makes it act like a different type. The standard library defines 3: `stack`, `queue`, and `priority_queue`. Each one is a class template that acts as wrapper to the underlying container (only a specific set of functions is provided), providing the functionality of a certain data structure (stack or queue). It's an interface to the underlying container. Each container adaptor provides its own operations (the only ones we can use), which make use of operations provided by the underlying container type (which we cannot use).

**Operations and types common to all container adaptors:**

- `size_type`: Type large enough to hold the size of the largest object of this type.
- `value_type`: Element type.
- `container_type`: Type of the underlying container on which the adaptor is implemented.
- `A a`: Create a new empty adaptor named a (default constructor) (`stack<int> stk`).
- `A a(c);`: Create a new adaptor named a with a copy of the container c (`deque<int> deq;` > `stack<int> stk(deq);`).
- `relational operators`: Each adaptor supports all relational operators (`==`, `!=`, `<`, `<=`, `>`, `>=`). They return the result of comparing the underlying containers.
- `a.empty()`: `false` if a has any elements, `true` otherwise.
- `a.size()`: Number of elements in a.
- `swap(a, b)` and `a.swap(b)`: Swap the contents of a and b.

**Defaults**:

- `stack` and `queue` use a `deque`, but can use `list` and `vector` as well.
- `priority_queue` use a `vector`, but can use a `deque` as well.
- We can override the default container type by naming a sequential container as a second type argument when creating the adaptor (examples: `stack<string, vector<string>> str_stk`, `stack<string, vector<string>> str_stk(svec)`).

**Constraints** on which container can be used for a given adaptor:

- All adaptors require the ability to add and remove elements. Thus, `array` is not valid.
- All adaptors require operations that add, remove, or access the last element. Thus, `forward_list` is not valid.
- `stack` requires only `push_back`, `pop_back`, and `back` operations. Thus, the remaining containers are valid.
- `queue` requires `back`, `push_back`, `front`, and `push_front`. Thus, `list` and `deque` are valid, but `vector` is not.
- `priority_queue` requires random access, `front`, `push_back`, and `pop_back`. Thus, `vector` and `deque` are valid, but `list` is not.

**Stack adaptor** (`<stack>`): Acts as a LIFO (last-in, first-out) data structure. The stack pushes and pops the element from the back of the underlying container (top of the stack). Provided operations:

- `s.pop()`: Remove, but don't return, the top element from the stack.
- `s.push(item)`: Create a new top element on the stack by copying or moving item.
- `s.emplace(args): Create a new top element on the stack by constructing it from args.
- `s.top()`: Returns, but doesn't remove, the top element on the stack.

**Queue adaptor** (`<queue>`): Acts as a FIFO (first-in, first-out) data structure. The queue pushes the elements on the back of the underlying container and pops them from the front. Provided operations:

- `q.pop()`: Removes, but doesn't return, the front element.
- `q.front()`: Returns, but doesn't remove, the front element.
- `q.back()`: Returns, but doesn't remove, the back element.
- `q.push(item)`: Create element with value item at the end of the queue.
- `q.emplace(args)`: Construct an element from args at the end of the queue.

**Priority queue adaptor** (`<queue>`): Queue where there's a priority among the elements held in the queue (by default, determined by `<` operator). Newly added elements are placed ahead of all the elements with lower priority. It provides constant time lookup of the largest (by default) element, at the expense of logarithmic insertion and extraction. A user-provided Compare can be supplied to change the ordering (e.g. using `std::greater<T>` would cause the smallest element to appear as the `top()`).

- `q.pop()`: Removes, but doesn't return, the highest-priority element.
- `q.top()`: Returns, but doesn't remove, the highest-priority element.
- `q.push(item)`: Create element with value item in its appropriate position.
- `q.emplace(args)`: Construct an element from args in its appropriate position.

```
stack<int> intStack;

for(size_t i = 0; i != 10; ++i)
  intStack.push(i);

while(!intStack.empty())
{
  int value = intStack.top();
  cout << value;
  intStack.pop();
}
```