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

```
int a1[] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
int a2[sizeof(a1) / sizeof(*a1)];   // alternative: std::size(a1)
auto ret = copy(begin(a1), end(a1), a2);   // returns iterator to one-past-the-last copied element
```

**Algorithms dependencies**:

- **Container independent**: Library algorithms operate on iterators, not containers, so algorithms cannot add or remove elements. They may change element's values and move them around, but never change container's size.
- **Element-type dependent**: Most of them use operations of the element type. However, most algorithms provide a way for us to supply our own operation to use in place of the default operator.

**Inserters** are a special class of iterators that can also execute insert operations on the underlying container. When an algorithm operates on one of them, the inserter can add elements, but the algorithm itself never does so.

### Read-only algorithms

They read, but never write, to the elements in their input range. Examples:

- `**find**(it1, it2, val)`: Uses `==` operator. Find an element in the input range.
- `**accumulate**(it1, it2, initialVal)`: Uses `+` operator. Add up all the elements in the input range. 
  - Note: Since strigs have `+` operator, this would concatenate the elements of a `vector<string>` (`accumulate(a, b, string("")`). Passing a string literal (`const char*`) as third parameter would be a compile-time error because it has no `+` operator.
- `**equal**(it1, it2, it3)`: Uses `==`. Check if two sequences are equal. It assumes that both sequences have same length ().

In algorithms that read elements from two sequences (like `equal`), the sequences be stored in different kinds of containers (as long as we are able to compare the elements), and the element types are not required to be the same type (as long as we can use the corresponding operator to compare the elements, like `vector<string>` and `list<const char*>`).

It's good practice to use `cbegin()` and `cend()` with read-only algorithms, unless you plan to use the returned iterator to change the element's value.

### Write algorithms

They can assign new values to the elements in their input range. We must ensure that the sequence is at least as large as the number of elements we ask the algorithm to write (otherwise, we get undefined result). Examples:

- `**fill**(it1, it2, val)`: Assign `val` to each element in the input range.
- `**fill_n**(it1, n, val)`: Assign `val` to `n` elements starting from `it1`.
- `**copy**(it1, it2, it3)`: Copy elements from its input range into elements in the destination.
- `**replace**(it1, it2, valA, valB)`: Replace all instances of `valA` with `valB`. Overwrites the original sequence.
- `**replace_copy**(it1, it2, it3, valA, valB)`: Like `replace`, but the new sequence is stored in `it3` (no overwrite).

**Insert iterator** (Inserter): Iterator that can add elements to a container (unlike normal iterators). When we assign through an insert iterator, a new element equal to the right-hand value is added to the container (assigning to a normal iterator assign to the element denoted by the iterator). Example:

- `back_inserter` (`<iterator>`): Function that takes a reference to a container and returns an insert iterator. Assigning through it calls `push_back` to add an element with the given value to the container.

```
vector<int> vec;
auto it = back_inserter(vec);
*it = 42;   // = vec.push_back(42)
```

```
vector<int> vec;
fill_n(back_inserter(vec), 10, 0);   // Appends 10 elements despite vec having size 0
```

```
vector<int> vec1(10);
vector<int> vec2;
replace_copy(vec1.cbegin(), vec1.cend(), back_inserter(vec2), 0, 42);   // Fills vec2 despite it has size 0
```

### Reorder algorithms

They rearrange the order of elements within a container. Examples:

- `**sort**()`: Sort (increasing order) elements using the element type's `<` operator.
- `unique(it1, it2)`: Move unique elements to the front. Return an iterator one past the unique range.

```
// Sort elements in alphabetical order and remove duplicates
void eliminateDuplicates(vector<string> &words)
{
  sort(words.begin(), words.end());   // sort alphabetically
  auto end_unique = unique(words.begin(), words.end());   // move unique elements to front
  words.erase(end_unique, words.end());   // remove non-unique elements
}
```

## Customizing operations

Many algorithms compare elements in the input sequence using, by default, either the element type's `<` or `==` operator. However, the library provides overloaded versions of these algorithms that let us supply our own operation. We can pass any kind of callable object to an algorithm.

**Callable object**: Object or expression (`e`) that let us apply the call operator (`()`) on it (`e(args)`) (`args` is a comma-separated list of zero or more arguments). Types of callables:

- Functions
- Function pointers
- Classes that overload the function-call operator
- Lambda expressions

### Passing a function to an algorithm

**Predicate**: Expression that can be called and that returns a value that can be used as a condition. Predicates used by library algorithms are either **unary** (have one parameter) or **binary** (have two parameters). Algorithms taking a predicate will call it on the elements in the input range (example: `sort` will use a binary predicate in place of `<`).

- `sort(it1, it2, callable)`
- `stable_sort(it1, it2, callable)`: Sort the input range maintaining the original order among equal elements.

```
bool isShorter(const string &s1, const string &s2)
{
  return s1.size() < s2.size();
}

**sort**(words.begin(), words.end(), isShorter);   // Sort by length (increasing size)
```

```
// Sort by size, and sort elements of same size alphabetically
eliminateDuplicates(words);   // Sort alphabetically and remove duplicates
**stable_sort**(words.begin(), words.end(), isShorter);
```

### Lambda expressions

Useful if our processing requires more arguments than the algorithm's predicate allows. Also useful for simple operations that we need in only one or two places.

**Lambda expression** (`[capture_list] (parameter_list) -> return_type { function_body }`): Callable unit of code. Unnamed, inline function. It has a return type, parameter list, and function body. Its elements are the same as in any ordinary function, except for the Capture list. It may be defined inside a function. We can omit either or both of the parameter list (no parameters) and return type (inferred from the returned expression), but must always include the capture list and function body. Lambdas cannot have default arguments. A lambda is called like a function by using the call operator, but omitting it is equivalent to specifying an empty parameter list.

**Capture list**: Comma-separated list (often empty) of local non-static variables from the surrounding (enclosing) function where the lambda appears. The lambda cannot use local variables not included in the list. However, it can use variables declared outside the function and local `static`s directly.

**Return type**: The return type can be specified with a trailing return (`-> return_type`). Otherwise, the compiler infers it, if all return statements yield expressions of same type. If a lambda contains any statement other than a `return`, it's inferred `void`. Return type must be declared explicitly when:

- Lambda contains multiple return statements that produce different types
- We need lambda to return a reference (without explicit declaration, lambdas always return by value)
- Complex logic and ambiguous inference

Examples:

- `transform(it1, it2, it3, callable)`: Call the callable on each element in the input sequence and write the result in a destination.

```
auto f = [] { return 42; };
cout << f() << endl;   // prints 42
```

```
stable_sort(
  words.begin(), words.end(), 
  [](const string &a, const string &b) { return a.size() < b.size(); } );
```

```
**transform**(
  vi.begin(), vi.end(),
  vi.begin(),
  [](int i) { return i < 0 ? -i : i; } );
```

```
auto f1 = [](int i) { return i < 0 ? -i : i; } );
auto f2 = [](int i) { if(i < 0) return -i; else return i; } );
auto f3 = [](int i) -> int { if(i < 0) return -i; else return i; } );

auto f4 = [](int i) { if(i < 0) return 1; else return 1.5; } );   // Compilation error (returns int and double)
auto f4 = [](int i)->double { if(i < 0) return 1; else return 1.5; } );
```

**Example**: Consider a list of words sorted by size (`vector<string> words`). Find the first element of size `m`.

- `**find_if**(it1, it2, callable)`: Returns iterator to first element for which the `callable` returns a nonzero value, or its `end` iterator if no such element is found.
  - `find_if(it1, it2, predicate)`: It takes a unary predicate. We cannot pass a second argument representing the size, so we cannot generalize the solution (we need one predicate per size).
  - `find_if(it1, it2, lambda)`: The lambda can use its capture list to store the size. This solution works for any size.

```
eliminateDuplicates(words);   // Sort alphabetically and remove duplicates
vector<string>::**size_type** sz = words.size();

**stable_sort**(   // Sort by size, like stable_sort(words.begin(), words.end(), isShorter)
  words.begin(), words.end(),
  [](const string &a. const string &b) {return a.size() < b.size();} );

auto wc = **find_if**(   // Find first element of size sz
  words.begin(), words.end(),
  [sz](const string &a) { return a.size() >= sz; } );
  
auto count = words.end() - wc;   // Number of elements of size >= sz

cout << count << " " << **make_plural**(count, "words", "s") << endl;

**for_each**(   // Print elements of size >= sz
  wc, words.end(),
  [](const string &s){cout << s << " ";} );
```

**Captured variables:**

When defining a lambda, the compiler generates a new unnamed class type corresponding to that lambda. Passing a lambda to a function defines both a new type and a new object of that type. When using `auto` to define a variable initialized by a lambda, we're defining an object of the type generated from that lambda. By default, the class contains a data member corresponding to the variables captured by the lambda, which are initialized when a lambda object is created. Variables can be captured by **value** (copied) or by **reference** (ensure the variables exist while lambda executes). Capture list **contents**:

- `[]`: Empty capture list.
- `[names]`: Comma-separated list of names local to the enclosing function. Captured by value by default. Names preceded by `&` are captured by reference.
- `[&]`: Implicit by reference capture list. Captures by reference all entities from the enclosing function used in the lambda body.
- `[=]`: Implicit by value capture list. Captures by value all entities from the enclosing function used in the lambda body.
- `[&, identifier_list]`: Like `[&]`, except for variables in `identifier_list`, which are captured by value (they must not be prefixed with `&`).
- `[=, reference_list]`: Like `[=]`, except for variables in `identifier_list`, which are captured by reference (they must be prefixed with `&`).

```
size_t v = 42;
auto fv = [v1] { return v; };
auto fr = [&v1] { return v; };
v = 0;
cout << fv();   // 42
cout << fr();   // 0
```

```
void biggies(vector<string> &words, vector<string>::size_type_sz, ostream &os = cout, char c = ' ')
{
  for_each(words.begin(), words.end(), [&os, c](const string &s) { os << s << c; } );
}
```

- We cannot copy `ostream` objects. We can only capture `os` by reference (or through a pointer to `os`).
- When passing a lambda to a function, it's executed immediately.

Functions can return callable objects. When returning a lambda from a function, it must not contain reference captures.

By default, a lambda may not change the value of a captured variable (except when it's a non-`const` captured by reference). To change this, it must follow the parameter list with keyword `mutable`.

```
size_t v = 42;
auto f1 = [v] () mutable { return ++v; }
auto f2 = [&v] { return ++v; }
v = 0;
cout << f1();   // 43
cout << f2();   // 1
```

**Binding arguments:**

When we pass a function to an algorithm (like `find_if(it1, it2, callable)`), sometimes we might want our function to accept additional arguments (like `size`). In this case, we can instead pass a lambda that uses its capture list to get these additional arguments (as explained previously). Alternatively, we can use `std::bind`.

`**bind**`: General-purpose function adaptor from `<functional>`. It takes a callable object and generates a new callable that "adapts" the parameter list of the original object. General form: `auto newCallable = bind(callable, arg_list)`. When we call `newCallable`, it calls `callable` passing the arguments in `arg_list` (comma-separated list of arguments).




502

## Revisiting iterators

## Structure of generic algorithms

## Container-specific algorithms

