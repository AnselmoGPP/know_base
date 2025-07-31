# Container basics

## Table of Contents
+ [Container library](#container-library)
+ [Operations](#operations)
+ [Definition and initialization](#definition-and-initialization)
+ [Iterators](#iterators)


## Container library

**Container**: Holds a collection of objects of a specified type. There're 2 main types (sequential and associative), which differ in how they organize their elements, which affect how elements are stored, accessed, added, and removed. 

- **Sequential (non-linked or linked)**: Holds elements whose position corresponds to the positions in which the elements are added to the container.

- **Associative (ordered or unordered)**: Holds elements whose positions depend on a key associated with each element.

**Adaptor**: It adapts a container type by defining a different interface to the container’s operations. The library provides 3 adaptors.

The container classes share a common interface, which each container extends in its own way. Each kind of container offers different set of performance and functionality trade-offs.

In general, each container is defined in a header file with the same name as the type (`<deque>`, `<list>`, etc.). The containers are **class templates**. We must supply additional information to generate a particular container type (usually, the element type).

Almost any type can be used as the element type of a **sequential container** (even another container).

```
list‹Sales_data› a;
deque‹double› b;
vector‹vector‹string›› c;
```

Some container operations require certain element types. We can define a container for a type that doesn’t support an operation-specific requirement, but won’t be able to use that operation.

Example: The sequential container constructor that takes a size argument uses the element type’s default constructor. If the element type has no default constructor, we won’t be able to construct a container using only an element count.

```
vector<noDefault> v1(10, init);
vector<noDefault> v2(10);          // error: No element initializer supplied
```


## Operations

Some operations are provided by all container types, others only by one type of container (sequential, associative, unordered associative), others are specific to a smaller subset of containers. The operations below are provided by all container types (unless declared otherwise).

**Type aliases**

- **Iterators**
  - `iterator`: Type of iterator for this container type
  - `const_iterator`: Iterator that can read but not change its elements
- **Sizes**
  - `size_type`: Unsigned int big enough to hold the size of the largest possible container of this type
  - `difference_type`: Signed type big enough to hold the distance between two iterators
- **Types**
  - `value_type`: Element type alias.
  - `reference`: Element’s lvalue type (i.e., `value_type&`)
  - `const_reference`: Element’s const lvalue type (i.e., `const value_type&`)
- **Construction**
  - `C c`: Default constructor, empty container
  - `C c1(c2)`: Construct c1 as a copy of c2
  - `C c(b, e)`: Copy elements from the range denoted by iterators b and e (not valid for `std::array`)
  - `C c{a,b,c...}`: List initialize c
- **Assignment**: All elements from one container are replaced with copies of elements from another container.
  - `c1 = c2`: Replace elements in c1  with those in c2
  - `c1 = {a,b,c...}`: Replace elements in c1 with those in the list (not valid for array)
  - `a.swap(b)` or `swap(a, b)` (preferred): Interchange contents of two containers. It's guaranteed to run in constant time since elements are not swapped (elements aren't copied, deleted, or inserted), internal data structures are swapped. Elements aren’t moved, so iterators, references, and pointers aren’t invalidated (iterators still refer to the same elements, but now in different containers). Exception: A swap on an `array` (`string`) do exchange elements, so it requires a time proportional to the number of elements, and it invalidates iterators, references, and pointers.
- **Size**
  - `c.size()`: Number of elements in c (not valid for forward_list)
  - `c.max.size()`: Maximum number (or bigger) of elements c can hold
  - `c.empty()`: false if c has any elements, true otherwise
- **Add/Remove elements** (not valid for std::array) (these operations’ interfaces varies by container type)
  - `c.insert(args)`: Copy element/s into c
  - `c.emplace(inits)`: Construct an element in c
  - `c.erase(args)`: Remove element/s
  - `c.clear()`: Remove all elements from c. Returns void
 - **Equality**
  - `==`,  `!=`: Equality operators
- **Relational operators**: Performs a pairwise comparison of elements.
  - `‹`,  `‹=`,  `›`,  `›=`: Relational operators (not supported by unordered associative containers)
- **Get iterators**
  - `c.begin()`,  `c.end()`: Return iterator to the first, one past the last element
  - `c.cbegin()`,  `c.cend()`: Return `const_iterator`
- **Reversible containers** (not valid for std::forward_list)
  - `reverse_iterator` (provided by most containers): Iterator that addresses elements in reverse order (inverts operators meaning).
  - `const_reverse_iterator`: Reverse iterator that cannot write the elements
  - `c.rbegin()`,  `c.rend()`: Return iterator to the last, one past the first element in c
  - `c.crbegin()`,  `c.crend()`: Return `const_reverse_iterator`

Examples:

```
list<string>::iterator iter;
vector<int>::difference_type count;
```

## Definition and initialization

Every container type defines a default **constructor**. It creates (except array) an empty container of the specified type. The other constructors take arguments that specify (except array) the size of the container and initial values of the elements.

**Initializing a container as a copy of another**

```
list<string> authors = {"John", "Steve", "Austen"}
vector<const char*> articles = {"a", "an", "the"}
```

Two ways:

- **Directly copy the container**: The container and element types must match (`list<string> list1(authors)`).

```
list<string> list2(authors);
deque<string> list3(authors);    // error: container type doesn't match
vector<string> words(articles);  // error: elements type doesn't match
```

**Copy a range of elements using 2 iterators** (array can’t): The container and element types can differ, as long as the elements can be converted (`deque<string> list2(authors.begin()+3, authors.end())`).

**List initialization**

```
list<string> authors = {"Milton", "Cervantes", "Austen"};
vector<const char*> articles = {"a", "an", "the"};
```

The initializer list implicitly specifies the size of the container (except the `array`).


## Iterators

### Ranges

Only a few library containers support subscript operator, but all of them define iterators (**string** is not a container type but also supports many container operations, including iterators). Like pointers, iterators give indirect access to an object (element in a container or character in a string) and let us move from one element to another. They can denote an element or position one past the last element, from where other iterator values are invalid. Types that have iterators have members that return iterators: `**.begin()**` (denotes first element), `**.end()**` (denotes position one-past-the-end, which is not an element, just a marker, and cannot be incremented or dereferrenced). If the container is **empty**, then `begin() == end()`.

**Iterator range**: Denoted by a pair of iterators (_begin_, _end_) that mark a range of elements from the container, each of which refers to an element, or to one-past-the-last-element, in the same container (_end_ must not precede _begin_). This is a **left-inclusive interval**: [_begin_, _end_).

```
while(begin != end) {
    *begin = val;
    ++begin;
}
```

### Standard container iterator operations

As with containers, iterators have a common interface. All of them support the following operations (one exception: forward_list iterators don’t support –):

```
*iter             // Dereference an iterator to get reference to element
iter->member      // Equivalent to (*iter).member
++iter, --iter    // Denotes next or previous element
iter1 == iter2
iter1 != iter2
```

Two iterators are **equal** if both denote the same element or both are off-the-end iterators (otherwise, they’re unequal). **Dereferencing** an invalid iterator or off-the-end iterator has undefined behaviour.

```
string s("my string");
if(s.begin() != s.end()) {         // if s is not empty
    auto it = s.begin();
    *it = toupper(*it);
}
```

```
for(auto it = s.begin(); it != s.end() && !isspace(*it); ++it)
     *it = toupper(*it);
```

All the library containers have iterators that define **==** and **!=** operators. Most don’t have **<** operator.

If an object has class type, we may access a **member** of that object.

```
for(auto it = text.cbegin(); it != text.cend() && !it->empty(); ++it)
    cout << *it << endl;
```

**Invalidations (of iterators, references, and pointers)**:

- **Changes in size** of a vector potentially invalidates all iterators into that vector. Loops that use iterators should not add elements to containers to which the iterator refer.
- **Assignment** related operations invalidate iterators, references, and pointers.
- **Swap** operations don’t change them (except strings), and the containers to which they refer are swapped (except arrays).

### Iterator types

```
list<string> a = {"John", "Jane", "Steve", "Sarah"}
```

- **iterator**: Can read and write.

```
auto it = a.begin();     // list<string>::iterator
auto it = a.end();
```

- **const_iterator**: May read but not write the element it denotes.

```
auto it = a.cbegin();    // list<string>::const_iterator
auto it = a.cend();
```

- **reverse_iterator**: Goes backward through a container and inverts the meaning of the iterator operations (example: saying ++ yields the previous element).

```
auto it = rbegin();      // list<string>::reverse_iterator
auto it = rend();
```

- **const_reverse_iterator**:

```
auto it = crbegin();     // list<string>::const_reverse_iterator
auto it = crend();
```

If a vector or string is **const**, we may use only the const_iterator type (begin() and end() return a const_iterator). If it is **non-const**, we may use iterator or const_iterator (begin() and end() return iterator). We can ask specifically for the const_iterator type with: cbegin() and cend(). We can convert a plain iterator to a const_iterator, but not vice versa. When write access is not needed, you should use cbegin() and cend().

When we use **auto** with begin() or end(), the iterator type we get depends on the container type.

```
list<string>::const_iterator it = a.begin();  // Explicitly specified
auto it = a.cbegin();                         // Depends on the container type
```

### Iterator arithmetic

**vector, string, deque & array ops**

Iterators for **string**, **vector**, **deque**, and **array** support additional operations:

```
iter + n
iter - n
iter += n
iter -= n
iter1 - iter2    // See below for explanation
>, >=, <, <=     // See below for explanation
```

`iter1 - iter2`: Yields the number that, when added to the right-hand iterator yields the left-hand iterator. Both iterators must refer to the same container. The result type is named `difference_type` (signed integral) (vector and string define it).

`iter1 < iter2`: Iterator A is less than iterator B if A refers to an element that appears in the container before the one denoted by B. Both iterators must refer to the same container.

The iterators must be valid and must denote elements in, or one past the end, of the same vector or string.

```
auto middle = v.begin() + v.size() / 2;    // element closest to midpoint
```

```
// Search the position of a certain string in a vector<string>
vector<string> text;
...
auto beg = text.begin(), end = text.end();
auto mid = text.begin + (end - beg)/2;
while(mid != end && *mid != sought) {
    if(sought < *mid)
        end = mid;
    else
        beg = mid + 1;
    mid = beg + (end - beg) / 2;
}
```
 