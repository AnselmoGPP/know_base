# C++ basics

## Table of Contents
+ [Basics](#basics)
+ [Flow of control](#flow-of-control)
+ [Return](#return)
+ [Variables](#variables)
+ [Built-in types](#built-in-types)
+ [Type conversions](#type-conversions)
+ [Compound types](#compound-types)
+ [const qualifier](#const-qualifier)
+ [Dealing with types](#dealing-with-types)
+ [Extern](#extern)
+ [Operators and expressions](#operators-and-expressions)
+ [Statements](#statements)
+ [Keywords, operators and punctuators](#keywords,-operators-and-punctuators)<<<
+ [Keywords](#keywords)<<<
+ [Identifiers](#identifiers)<<<
+ [Preprocessor directives](#preprocessor-directives)<<<
+ [References](#references)


## Basics

C++ provides a set of built-in types, operators to manipulate those types, a few statements for program flow control, and mechanisms that allow to define new data structures.

C++ provides a rich set of operators and defines what they do when applied to operands of built-in type. It also allows us to define the meaning of most of the operators when applied to operands of class types.

### Main terms

- **Expression**: Smallest unit of computation. One or more operands and usually one or more operators. It is evaluated to produce a result (i + j, assuming i and j are ints). Simplest for: single literal or variable.

- **Compound expression**: Expression with 2 or more operators.

- **Statement**: Composed of one or more operands and (usually) an operator. Yields a result.

- **Variable**: Named object.

- **Declaration**: Asserts the existence of a variable, function, or type defined elsewhere. Names may not be used until they are defined or declared.

- **Definition**: Allocates storage for a variable of a specified type and optionally initializes the variable. Names may not be used until they are defined or declared.

- **Preprocessor**: Program that runs before the compiler and changes the source text of our programs. Example of preprocessor facilities: `#include`, header guards, namespaces, etc.

- **C++ Standard library**: Collection of classes and functions. Provides generic containers, functions to utilize and manipulate these containers, function objects, generic strings and streams (including interactive and file I/O), support for some language features, and functions for everyday tasks. Also incorporates the **C library**. Headers in C have names ending in **.h**. C++ versions of these C headers are named **cname**, without .h. Names from the C++ library (not C library) are declared within the **std** namespace. Use the C++ versions of C library headers. They have similar contents, but in a form appropriate for C++ programs

- **Template**: Instructions to the compiler for generating classes or functions. When we use a template, we specify what kind of class or function we want the compiler to instantiate by supplying additional information, which nature depends on the template (supply it inside angle brackets, following the template’s name.

- **Instantiation**: Process the compiler uses to create a class or function from a template.

- **Undefined behaviour**: Results from error that the compiler is not required or not able to detect. Programs with these problem can appear to execute correctly in some circumstances and/or on some compilers.

- **Implementation-defined behaviour**: Programs with this problem are nonportable. Such as assuming that the size of an int is a fixed and known value.

- **Compilation**: 

  - **Preprocessing**: The preprocessor takes a C++ _source code_ file and deals with the preprocessor directive (`#include`, `#define`, …). Outputs a C++ file without preprocessor directives.
  - **Compilation**: Compiler takes the preprocessor’s output and produces an _object file_.
  - **Linking**: The linker takes these object files and produces either a _library_ or an _executable file_.

### Namespaces

The Standard Library names are in the **std** namespace.

**Scope operator** (`::`): Says the compiler should look in the scope of the left-hand operand for the name of the right-hand operand. Example: `std::cin`.

**using** declaration lets us use a name from a namespace directly, without applying the scope operator. Example: `using namespace::name`

```
using std::cin;
cin >> i;
```

**Code inside headers should not use using declarations**. They are copied into the program’s text and may cause unexpected name conflicts.

### Compiling

We write the source code in `hpp` (headers) and `cpp` (source code) files. Compiler translates the source code into machine code that the computer can understand and run. Header files (`hpp`) are not compiled, they are just copied into `cpp` files. Only `cpp` files are compiled, which results in a bunch of `obj` files, one per `cpp` file.

In `VS` the `Compile` button (`F7`) compiles. The compiler can output compilation errors messages (like `C2143: Syntax error`).

1. We write simple **text files** (`hpp` and `cpp` files) using C++ programming language.

2. **Preprocessing**: Compiler substitutes all the preprocessor statements that are in our code with whatever are the contents they refer (`include`, `define`, `if`, `ifdef`, …). This transforms the `cpp` file into a **translation unit** (TU).
  - `include`: Copies whatever is the content of the header in your code.
  - `define`: Substitutes a given sequence of letters by another sequence of letters.
  - `if`, `endif`: Include or exclude code based on a given condition.
  - etc.

3. **Abstract syntax tree**: Sort the code (by tokenizing and parsing) to a format compiler understands.

4. **Object files (`obj`)**: Compiler creates it from our C++ preprocessed code (one `obj` per `cpp` file). It contains the machine code (assembly instructions and constants) the CPU will actually execute when running our program. 

  - **Optimization**: Compiler may optimize your code to improve its performance (example: it may get rid of useless instructions)
  - **Debug mode**: Code is not optimized, is made verbose, and is made easier to debug.
  - **Constant folding**: Compiler works out anything that is constant (example: `5 * 2` becomes `10`).

### Linking

The **linker** links all the `obj` files into one executable binary that contains all the machine code that we need to run. Its main purpose is to find where each symbol is. It also finds where the entry point is (usually `main()`).

**Symbol**: Name representing an entity in the code (variable, function, class, object...). 

In `VS`, the `Build` button (`F5`) compiles and links. The linker can output linking error messages (like `LNK1561: Entry point must be defined`).

`Error: Unresolved external symbol`: Error that occurs when the linker cannot find something that it needs. Example: a function called in a TU is not defined in any of the existing TUs.

If a function is defined in a TU, the compilation will include it in the corresponding `obj` file so it can be used elsewhere, unless it is `static` and not used in TU.

Functions have to be different to each other in the name, return value, and/or parameters.

`LNK1169: One or more X defined symbols found`: A symbol X is defined more than once in a TU. Example: the same function is defined in `A.cpp` and `B.hpp`, and A includes B (`#include <B.hpp>`). Depending on the situation, there're different solutions:

- Put the duplicated code in just one TU.
- Use `static`: Makes a function to be only declared for the current TU.
- Use `inline`: Makes a function body to replace the code that called it. 

### Stack and Heap

Stack and Heap are different types of memory. Both are **stored** in the computer’s RAM. The **stack** is much faster than the **heap** because allocating memory in the stack only requires to move the pointer up.

In a **multithreaded** application, each thread will have its own stack, but all of them will share the same heap. There must be some coordination between them so that they don’t try to access and manipulate the same piece of memory in the heap.

How to **store in the stack**: If you create an object inside a function without using the “new” operator then this will create and store the object on the stack, and not on the heap.

```
Type var;
```

How to **store in the heap**: If you create an object inside a function using the `new` keyword, it will be created on the heap. But, since it’s created using `new`, we must `delete` the object on our own as well (otherwise, we will end up with a memory leak).

```
Type* var = new Type( );
delete var;
```

In C, data can be stored in the stack dynamically using `alloca()`: `char *message = (char*)alloca(length * sizeof(char))`.

**Existence**: Once a function call runs to completion, any data on the stack created specifically for that function call will automatically be deleted (it goes out of scope). Any data on the heap will remain there until it’s manually deleted.

**Growth in size**: The stack has a fixed size and cannot grow (stack overflow) (although some languages have extensions that allow this). The heap can grow (the OS can add more memory to it) if more memory is needed.

The stack and heap **implementation** is dependent on the language, compiler and run-time. But, in general, both are used in for the same things in any language.

**Memory deallocation**: Data on the stack is automatically deallocated when variables go out of scope. Data on the heap has to be deleted manually (free, delete, delete[]…) in some languages (C, C++…), but others (Java, .NET…) use garbage collection to automatically delete it.

**Problems**: If the stack runs out of memory, a stack overflow happens and your program crashes. If data in the heap is stored in non-contiguous blocks (fragmentation), allocating new memory may be impossible (there’s enough memory but not a block big enough).

**Usage**: The stack is small, so you will use it when you know how much memory you will need or if you know the size of your data is very small. You will use the heap when you don’t know how much memory you will need (dynamic array…) or if you know that you will need a lot of memory for your data.

### Headers

Classes are usually defined in a **header file**. Headers from the standard library are enclosed in angle brackets (`<>`), other libraries in double quotes (`""`).

#### #include

Preprocessor directive that makes preprocessor replace the #include with the contents of the specified header.

We can define a class inside a function (limited functionality). When defined outside a function, there may be only one definition of that class in any given source file. If we use a class in several files, its definition must be the same in each file, so classes are usually defined in header files. Headers usually contain entities that can be defined only once in any given file and often need to use facilities from other headers.

**Difference between `#include <…>` and `#include "…"`**

The difference is in the location where the preprocessor searches for the included file.

- **`#include <filename>`**: The preprocessor searches in an implementation dependent manner, normally in search directories pre-designated by the compiler/IDE. This method is normally used to include standard library header files.

- **`#include "filename"`**: The preprocessor searches first in the same directory as the file containing the directive, and then follows the search path used for the `#include <filename>` form. This method is normally used to include programmer-defined header files.

#### Header guards

Used for making safe to include a header multiple times. Header guards rely on some preprocessor variables. They can have 2 possible states: defined or not defined.

- `#define`: Takes a name and defines it as a preprocessor variable.
- `#ifdef`: It’s true if the variable has been defined.
- `#ifndef`: It’s true if the variable has not been defined.
- `#endif`: If #ifdef or #ifndef is true, everything following the it is processed up to the matching #endif.

```
#ifndef MYCLASS_H
#define MYCLASS_H

#include <string>

struct MyClass {
std::string number;
};

#endif
```

Preprocessor variables must be unique throughout the program (they don’t respect C++ scoping rules). That’s why we base the guard’s name on the name of a class in the header. Preprocessor variables usually are written in all uppercase.

#### Including platform-dependent code

OS and architecture dependent code:

```
#ifdef _WIN32
  ##ifdef _WIN64
    // ...
  ##else
     // ..
  ##endif
#elif defined(__linux__)
  ##ifdef __x86_64__
    // ...
  ##elif defined(__i386__)
    // ...
  ##endif
#elif defined(__APPLE__) && define(__MACH__)
  ##ifdef __x86_64__
    // ...
  ##elif defined(__i386__)
    // ...
  ##endif
#endif
```

### Directive

A **directive** or **pragma** is a language construct that specifies how a compiler (or other translator) should process its input. Directives are not part of the grammar of a programming language, and may vary from compiler to compiler. They can be processed by a **preprocessor** to specify compiler behavior, or function as a form of in-band parameterization. A directive does not perform any action in the language itself, but rather only a __change in the behavior of the compiler__.

In some cases directives specify global behavior, while in other cases they only affect a local section (such as a block of programming code). In some cases, directives are optional compiler hints, and may be ignored, but normally they are prescriptive, and must be followed.

**#pragma once**:

In C and C++, `#pragma once` is a non-standard but widely supported preprocessor directive designed to cause the current source file to be included only once in a single compilation. Thus, `#pragma once` serves the same purpose as `#include guard macro`, but with several advantages, including: less code, avoidance of name clashes, and sometimes improvement in compilation speed

```
#pragma once         // Usually used in top of headers
```

**#pragma pack**:

**Bit padding**: It is the addition of one or more extra bits to a transmission or storage unit to make it conform to a standard size.

Basically, the compiler, unless otherwise directed, will line up structure members on 2 byte or 4 byte boundaries (this makes it easier and faster for the processor to handle). So the structure contains secret padding bytes to make this happen. The pragma pack directive (in Microsoft compiler) allows you to change this alignment scheme.

Some things (particularly in relation to hardware) do not have the luxury to waste bytes like this and they send their data in an exact fit. This means that it is not wise to read data from a hardware device directly into a normal structure. If you want to read data that fit exactly into a structure, you can tell the compiler to make the structure an exact fit like this.

```
#pragma pack(push, 1)     // Exact fit, no padding
struct MyStruct {
    char a;
    int b;
    int array[2];
};

#pragma pack(pop)         // Back to whatever the previous packing mode was
```

Without pragma directive, this struct is 16 bytes (4*4). With the packing of 1, the size is 13.


### Data alignment & Padding

#### Data alignment

Every object type has the property called alignment requirement, which is an integer value (of type std::size_t, always a power of 2) representing the **number of bytes between successive addresses at which objects of this type can be allocated**.

- [Object alignment](https://en.cppreference.com/w/cpp/language/object#Alignment): Number of bytes between successive addresses at which objects of this type can be allocated.
- [Data alignment](http://www.songho.ca/misc/alignment/dataalign.html): The address of a data can be evenly divisible by 1, 2, 4, or 8. In other words, data object can have 1-byte, 2-byte, 4-byte, 8-byte alignment or any power of 2.
- [Alignment (VS)](https://docs.microsoft.com/es-es/cpp/cpp/alignment-cpp-declarations?view=msvc-160): By default, the compiler aligns class members on their size value (`bool`, `char`: 1 byte. `short`: 2 bytes. `int`, `long`, `float`: 4 bytes. `long long`, `double`, `long double`: 8 bytes).
- [alignas operator](https://en.cppreference.com/w/cpp/language/alignas): Specifies the alignment requirement of a type or object.
- [alignof operator](https://en.cppreference.com/w/cpp/language/alignof): Queries alignment of a type.

#### Bit padding

Bit padding is the addition of one or more extra bits to a transmission or storage unit to make it conform to a standard size.


## Flow of control

Statements usually execute sequentially. Some flow-of-control statements allow for more complicated execution paths. Types:

- **Iteration (loop)**: Repeats execution until a condition is true.
  - While
  - Do while
  - For
  - Range for
- **Selection (condition)**: Executes if a condition is true.
  - If
  - Switch
  - Ternary <<<
- **Jump**
  - Break
  - Continue
  - Return <<<
  - Goto

### Iteration

#### While

Repeatedly executes a section of code so long as a given condition is true (bool). Tests condition before executing the body. Useful for iterating indefinitly or for accessing to the value of the control variable after the loop finishes.

Tests the condition > If true, executes the statement > Repeats until condition is false

```
while (condition)
    statement
```

**Condition**: Expression or initialized variable declaration. It may not be empty. Ordinarily, the condition or the loop body must change this expression; otherwise, the loop might never terminate.

Variables defined in a while condition or while body are created and destroyed on each iteration.

```
while (val <= 0) {
    sum += val;
    ++val;
}
```

```
while (cin >> value) ...
```

The while tests the stream until it encounters **end-of-file** or an **input error**. Different operating systems use different conventions to enter end-of-file. Usually:

- __Windows__: Ctrl-z + Enter or Return.
- __UNIX, Mac OS X__: Ctrl-d.

#### Do While

Executes the body and then tests its condition. Like a while, but condition is tested after the statement body completes. Ends with a semicolon.

```
do
    statement
while (condition);
```

- **Statement**: Executed before condition is evaluated.
- **Condition**: Cannot be empty. Cannot contain variable definitions. Variables used here must be defined outside the body.

```
string str;
do {
    cout << "Enter 2 values: ";
    int a = 0, b = 0;
    cin >> a >> b;
    cout >> "For more, enter yes or no: ";
    cin >> str;
} while (!str.empty() && str[0] != 'n');
```

#### For

Control how often the body is executed. Test condition before executing the body. The header has 3 parts:

```
for(init-statement; condition; expression)
    statement
```

- **Init-statement**: Executed only once. Must be declaration statement, expression statement, or null statement. Usually initialize or assign a starting value modified during the loop. Can define several objects (use comma) but can only be a single declaration statement, so all variables must have same base type.
- **Condition**: Tested each time through the loop (loop continues until condition fails). If false, statement is not executed.
- **Expression**
- **Statement**: Single or compound statement.

```
for (int i = 0; i < 10; ++i) {...}
```

Execution flow: init-statement/expression > Condition > Statement

Any object **defined** within the for header is limited to the body of the for loop.

A for header can **omit** any or all of init-statement, condition, expression or statement by using a null statement (single semicolon). Omitting condition is equivalent to writing true as the condition.

#### Range for

Iterates through the elements in a given sequence and performs some operation on each value. Execution ends when all the elements have been processed.

```
for (declaration : expression)
    statement
```

- **Expression**: Represent a sequence: braced initialized list, array, or an object that has begin and end members that returns iterators (such as vector or string).
- **Declaration**: Defines a variable. It must be possible to convert each element of the sequence to the variable’s type.

To modify the value of the elements in a sequence, you must define the loop variable as a reference type:

```
for (auto &c : str)
    c = toupper(c);
```

The body of a **range for** must not change size of the sequence over which it is iterating (example: It cannot add elements to a vector).

To avoid copying the sequence, you can define the loop variable as const reference:

```
for(const auto &s : text) { ... }
```

### Selection

#### If

A conditional execution like while, but without loop. Executes an statement based on whether a specified condition is true.

```
if (condition)
    statement_1
else
    statement_2
```

```
if (std::cin >> val) {...}   // These statements can be blocks
else {...}
```

Both, “=” (assignment) and “==” (equality) operators can appear inside a condition.

**Condition** must be enclosed by parentheses. It can be an expression or an initialized variable declaration. Must have a type convertible to bool.

```
if (condition_2)        // Nested ifs
    statement_1
else if (condition_2)
    statement_2
else ...
```

**Dangling else**: When we nest an _if_ inside another _if_, it’s possible that there will be more _if_ branches than _else_ branches. How do we know to which _if_ a given _else_ belongs? Each _else_ is matched with the closest preceding unmatched if.

```
if(grade % 10 ≻= 3)
    if(grade % 10 ≻ 7)
        grade += '+';
    else
        grade += '-';
```

We can make the else part of the outer _if_ by enclosing the inner _if_ in a block.

```
if(grade % 10 ≻= 3) {
    if(grade % 10 ≻ 7)
        grade += '+';
} else 
    grade += '-';
```

#### Switch

Way of selecting among a number of fixeed alternatives. Evaluates an integral expression and chooses one of several execution paths.

```
switch (ch) {
    case 'a':
        ++counter;
        break;
    case 'b':
        ++counter;
        break;
    case 'c':
        ++counter;
        break;
    default:
        --counter;
        break;
}
```

Evaluates the parenthesized expression. That expression may be an initialized variable declaration. It is converted to integral type. If it matches the value of a case label, execution begins from there until the end of the switch or until a **break**.

- **case**: This keyword and the associated value is the **case label**. It must be __integral constant expression__. Can only have a single value.
- **break**: Interrupts the current control flow. If you omit a break, explain the logic.
- **default**: Special label executed when no case label matches the value of the switch expression. An empty default (must be followed by null statement or empty block) indicates that the case was considered.

```
char ch = get_val();
int val = 32;
switch(ch) {
    case 3.14:     // error (non-integer)
    case val:      // error (non-constant)
    ...
```

Any code inside the switch before the activated label is ignored. What happens if the skipped code includes a variable definition? It’s illegal to jump from a place where a variable with an initializer is out of scope to a place where it is in scope. You can only declare it previously, but not initialize it previously.

```
switch (x) {
    case true:
        string file_name;     // error (implicitly initialized)
        int val_1 = 0;        // error (explicitly initialized)
        int val_2;            // ok (not initialized)
        break;
    case false:
        val_2 = next_num();         // ok
        if(file_name.empty()) ...   // error (file_name is in scope but wasn't initialized
        break;
}
```

It’s illegal to jump over an initialization if the initialized variable is in scope at the point to which control transfers. If we need to define and initialize a variable for a particular case, we can define the variable inside a block.

```
case true:
    {
        string file_name = get_file_name();
    }
```

#### Ternary

```
int a = 5, b = 10;
int largestumber;
largestNumber = (a > b) ? a : b;
```

### Jump

#### Break

Interrupts the current control flow. It can only affect the nearest enclosing loop or switch. Terminates the nearest enclosing while, do while, for or switch.

#### Continue

Terminates the current iteration of the nearest enclosing loop and begins the next iteration. Can only appear inside a for, while or do while, including inside statements or blocks nested inside these loops. May appear inside a switch only if it’s embedded inside an iterative statement.

#### Return

The return statement terminates the function that is currenty executing and returns control to the point from which the function was called.  Learn more [**here**](#return).

#### Goto

Unconditional jump from the goto to another statement in the same function. Programs should not use goto (harder to understand and to modify). Allows jumping backwards.

```
goto label_A;
...
label_A: return;          // labeled statement
```

- **Label**: Identifier that identifies a statement.
- **Labeled statement**: Any statement preceded by an identifier followed by a colon. Independent of names used for variables and other identifiers.

It cannot transfer control from a point where an initialized variable is out of scope to a point where that variable is in scope.

```
goto end;
int a = 5;
end:
    a = 42;    // error (code uses a but bypassed its declaration)
```

Jumping back to a point before a variable is defined destroys the variable and constructs it again:

```
begin:
int b = get_size();
if (b ≺= 0)
    goto begin;
```


## Return

The return statement terminates the function that is currenty executing and returns control to the point from which the function was called. Two forms: `return;` and `return expression;`.

### Functions with no return value

A return with no value may be used only in a function that returns `void`, although it doesn’t require to contain a return. It’s usually used to exit the function in an intermediate point. It may return the result of another function that returns void.

### Functions that return a value

Every return in a function with a return type other than void must return a value, and it must be the same type as the function return type or a type that can be implicitly converted.

Values are returned in exactly the same way as variables and parameters are initialized: The return value (result of the function call) is used to initialize a temporary at the call site.

Remember the initialization rules in functions that return local variables. Examples of return types:

- `string` > The returned value is copied to the call site
- `const string &` > The returned value is not copied

Never return local objects or pointer to local objects

#### Functions that return class types

The call operator () has associativity and precedence (same precedence as dot and arrow operators and left associative like them). If a function returns a pointer, reference of object of class type, we can use the result of a call to call a member of the resulting object.

```
auto sz = shorterString(s1,s2).size();
```

Calls to functions that return references are **Lvalues**. Other return types yield **rvalues**. A call to a function that returns a reference can be used in the same way as any other lvalue. Example: We can assign to the result of a function that returns a reference to nonconst.

```
char &getVal();

void func() {
    getVal() = 'A';   // Return value is a reference, so the call is an lvalue
}
```

If the return type is a reference to const, we may not assign to the result of the call.

#### List initializing the return value

Functions can return a braced list of values. If the list is empty, that temporary is value initialized. Otherwise, the value of the return depends on the function’s return type.

```
vector<string> process() {
    // ... expected and actual are strings
    if(expected.empty()) return {};                         // return empty vector
    else if(expected == actual) return {"hello", "okay"};   // return list-initialized vector
    else return {"hello", expected, actual};
}
```

In a function that returns a built-in type, a braced list may contain at most one value, and that value must not require a narrowing conversion. If the function returns a class type, that class defines how the initializers are used.

#### Return from main

A function with a return type other than void must return a value. However, main() is an exception because when control reaches the end of main() and there is no return, then the compiler implicitly inserts a return of 0.

A value returned from main() is trated as a status indicator (0 is success, other values are failure). A nonzero value has machine dependent meaning. To make return values machine independent, <cstdlib> defines 2 preprocessor variables that can be used to indicate success or failure:

```
int main() {
    if(some_failure) return EXIT_FAILURE;
    else return EXIT_SUCCESS;
}
```

#### Recursion

A recursive functions calls itself, either directly or indirectly.

```
int factorial(int val) {
    if(val > 1) 
        return factorial(val-1) * val;
    return 1
}
```

There must always be a path through a recursive function that doesn’t involve a recursive call; otherwise, the function will recurse forever (until the program stack is exhausted). Main() may not call itself.

#### Returning a pointer to an array

Because we cannot copy an array, a function cannot return an array, but it can return a pointer or reference to an array. The most straightforward way is to use a type alias.

```
typedef int arrT[10];     // arrT is a synonym for the type array of 10 ints
using arrT = int[10];     // equivalent to the previous
arrT* func(int i);        // function that returns a pointer to an array of 10 ints
```

#### Declaring a function that returns a pointer to an array

Remember that, without using a type alias, we must remember that the dimension of an array follows the name being defined.

```
int arr[10];       // array of 10 int
int * p1[10];      // array of 10 pointers
int (*p2)[10];     // pointer to an array of 10 ints
```

```
type (*function(parameter_list))[dimension]
```

The parentheses are necessary for the same reason as with p2. Without them, we would be defining a function that returns an array of pointers.

Declaration of func without using type alias:

```
int (*func(int i))[10];
     // func(int) -> We call this function.
     // (*func(int)) -> We dereference the result of that call.
     // int (*func(int))[10]) -> Dereferencing the result of func yields an array of type int and size 10.
```

#### Using a Trailing return

Can be defined for any function, but is most useful for functions with complicated returns (such as pointers or references to arrays). It’s another way to simplify the declaration of func.

```
auto func(int i) -> int(*)[10];        // func returns a pointer to an array of 10 ints
```

#### Using decltype

An alternative is to use decltype to declare the return type. decltype doesn’t automatically convert an array to its corresponding pointer type, we must add a *.

```
int odd[] = {1,3,5,7,9};
int even[] = {0,2,4,6,8};
decltype(odd) *arrPtr(int i) {
    return (i % 2) ? &odd :: &even;    // returns a pointer to the array
}
````


## Variables

**Variable/object**: Named storage that our programs can manipulate. It has a type that determines the size and layout of the variable’s memory, range of values that can be stored there, and set of operations that can be applied on it.

**Object**: Generally, it’s a region of memory that can contain data and has a type. However, sometimes is used with different meanings:

- Variables or values of class types
- Named objects
- Data that can be changed by the program (consider value as data that is read-only)

### Initialization

**Initialization**: A value is given to a variable when it is created.

**Assignment**: Obliterates an object’s current value and replaces that with a new one.

Several forms of initialization:

```
int item = 0;
int item = {0};
int item{0};
int item(0);
```

**List initialization**: When curly braces are used for initialization. Compiler will not let list initialize variables of built-in type if the initializer leads to loss of information.

```
long double val = 2,71828;
int a{val}, b = {val};          // errors
int c(val), d = val;            // ok, but truncated
```

**Default initialization**: It’s when you define a variable without an initializer. Variables defined outside any function body are initialized to zero (with one exception), but inside a function are uninitialized, so its value is undefined (so, it’s recommended to initialize every object of built-in type). Each class controls how we initialize objects of that class type.

**Declaration**: Makes a name known to the program. Specify type and name. Allocates storage and may provide an initial value. Variables must be defined only once but can be declared many times.

**Definition**: Creates the associated entity.

### Identifier

Name of a variable.

- Can be composed of letters, digits and the underscore character
- No length limits
- Case-sensitive
- Must begin with letter or underscore (identifiers defined outside a function cannot begin with underscore)
- Cannot begin with underscore followed immediately by uppercase letter
- Cannot contain 2 consecutive underscores
- You cannot use names of keywords, alternative operators or reserved names from the standard library

Conventions for naming variables:

- Identifier should have some meaning
- Variable names > Usually lowercase
- Classes names > Usually begin with uppercase
- Identifiers with multiple words should distinguish each (deep_blue, deepBlue)

### Scope

Part of the program where a name has a particular meaning. Most scopes are delimited by **curly braces**. The same name can refer to different objects in different scopes. Names are visible from the point where they are declared until the end of the scope in which the declaration appears.

Names declared at the **global scope** are accessible throughout the program. Names declared inside a block have **block scope**.

**Nested scopes**: Scopes can contain other scopes (**inner scope**, **outer scope**). A name declared in one scope can be used in inner scopes. Names declared in a scope can also be redefine in an inner scope.

```
int test = 5;
int main() {
    int test = 8; // new local test hides the global test
    std::cout << ::test; // outputs the global test
}
```

The global scope has no name, so the **scope operator** with empty left side is a request to the global scope.


## Built-in types

The type of an object determines what that data means and what **operations** can be performed on it. C++ is a **statically typed language**: type checking is done at compile time, so compiler must know the type of every name used in the program before it is used.

**Byte**: Smallest chunk of addressable memory. Set of 8 bits.

**Word**: Basic unit of storage. Usually, a small number of bytes.

### Arithmetic types

Two types: **integral** and **floating-point** types.  The number of bits in arithmetic types varies across machines. The standard guarantees **minimum sizes**:

- Integral types:

  - `bool`: NA
  - `char`: 8
  - `wchar_t`: 16
  - `char16_t`: 16
  - `char32_t`: 32
  - `short`: 16
  - `int`: 16
  - `long`: 32
  - `long long`: 64

- Floating-point types:

  - `float`: 6 significant digits
  - `double`: 10 significant digits
  - `long double`: 10 significant digits

On most machines, a byte contains 8 bits and a word 32 or 64 bits (4 or 8 bytes). Most computers associate a number (**address**) with each byte in the memory. We can use an address to refer to any of several variously sized collections of bits starting at that addres. The type determines how many bits are used and how to interpret them. If the object at location 348659 has type float and it is stored in 32 bits on this machine, then the object at that address spans the entire word.

`**float**`: Usually represented in 1 word, doubles in 2, and long doubles in 3-4 words. Floats tipically yield 7 significant digits, and doubles 16.

`**int**`: They may be signed (by default) or unsigned (adding “signed”), except for bool and the extended character types.

`**char**`: Depending on the compiler, char may be signed or unsigned by default (usually, signed). An 8-bit unsigned char holds values from range [0, 255]. An 8-bit signed char is guaranteed to hold [-127, 127] but usually is [-128, 127].

### Literals

They have a self-evident value. The form and value of a literal determine its type.

If it starts with **0**, it’s interpreted as **octal**. If starts with **0x** or **0X**, it’s interpreted as **hexadecimal**.

- **Decimal** literals: Signed by default. Size is the smallest type of int, long, long long where it fits.
- **Octal / hexadecimal** literals: Can be signed or unsigned. Size is the smallest type of int, unsigned int, long, unsigned long, long long, unsigned long long where it fits.

We can override these defaults by using a prefix or suffix:

- Prefix:

  - `char16_t`: u
  - `char32_t`: U
  - `wchar_t`: L
  - `char`: u8

- Suffix:

  - `unsigned`: u or U
  - `long`: l or L
  - `long long`: ll or LL
  - `float`: f or F
  - `long double`: l or L

Decimal, octal or hexadecimal:

- **with suffix U**: Size is the smallest type of `unsigned int`, `unsigned long`, `unsigned long long` where it fits.
- **with suffix L**: Size is at least `long`.
- **with suffix LL**: Size is either `long long` or `unsigned long long`.

We can combine U with L or LL (UL will be `unsigned long` or `unsigned long long`, depending where the value fits).

**Decimal literals**: They never have negative values. The minus sign is just an operator that negates the literal.

**Floating-point literals**: They include a decimal point or an exponent (E or e). They are `double` by default.


```
3.14159     3.14159E0     0.     0e0     .001
```

**Literal of type char**: Character enclosed within single quotes.

**Character string literal**:Zero or more characters enclosed between double quotation marks. Type: array of constant chars. Compiler appends a null character (‘\0’) to every string literal. Two string literals that appear adjacent to one another and separated only by spaces, tabs or newlines are concatenated into a single literal.

**Escape sequence**:

Begins with a backslash. Use it as if it were a single character.

- `\n`: Newline
- `\v`: Vertical tab
- `\t`: Horizontal tab
- `\\`: Backslash
- `\r`: Carriage return
- `\b`: Backspace
- `\?`: Question mark
- `\f`: Formfeed
- `\a`: Alert (bell)
- `\”`: Double quote
- `\’`: Single quote

__Carriage return (`\r`)__ (CR, 0x0D) moves the cursor to the beginning of the line without advancing to the next line. Note: there is no portable way to go to the previous line (link).

__Line feed (`\n`)__ (LF, 0x0A) moves the cursor down to the next line without returning to the beginning of the line. This character is used as the new line character in Unix based systems (Linux, Android, macOS X, etc).

__End of Line (`\r\n`)__ (EOL, 0x0D0A) is actually two ASCII characters. It moves the cursor both down to the next line and to the beginning of that line. Used as the new line character in most other non-Unix operating systems (Windows, Symbian…).

**Generalized escape sequences**: Uses octal or hexadecimal values. The value represents the numerical value of the character.

- `\x` followed by one or more hexadecimal digits
- `\` followed by one, two or three octal digits. Only the first three are considered.

```
\0 (null)  \7 (bell)  \12 (newline)  \40 (blank)  \115 ('M')  \x4d ('M')
std::cout << "\115I\x4dO";         // prints MIMO
```

**Boolean**: Words `true` and `false` are literals of type bool. Word `nullptr` is a pointer literal.

### ASCII characters

<br>![ascii_table](https://raw.githubusercontent.com/AnselmoGPP/Learn_Computer_Science/master/topics/cpp/resources/asciifull.png)


## Type conversions

### Implicit conversions

They happen automatically when we use an object of one type where another type is expected. When we assign an incorrect type to another:

- `bool = any`: `false` if value is 0, `true` otherwise.
- `any = bool`: 1 value if `true`, 0 value if `false`.
- `integral = floating`: Value truncated (part before the decimal point is omitted).
- `floating = integral`: Fractional part is 0 (precision may be lost if integer has more bits).
- `unsigned = out-of-range`: Remainder of value modulo the number of values the target type can hold.
- `signed = out-of-range`: Undefined.

Compiler also applies these conversions to arithmetic values in other situations, like conditions (nonbool value as a condition > converted to bool).

- `unsigned` and `signed` in same arithmetic expression: Signed is ordinarily converted to unsigned.

Two types are **related** if there is a conversion between them. When 2 types are related, we can use an object or value of one type where an operand of the related type is expected.

```
int val = 3,14 + 3;        // 6
```

Implicit conversions transforms the operands to a common type automatically. Implicit conversions among arithmetic types are defined to preserve precision, if possible (if an expression has integral and floating-point operands, the integer is converted to floating-point). **Initialitation** happens next: the type of the object we are initializating dominates and the initializer is converted to the object’s type (the double result of the addition is converted to int and used to initialize val).

Compiler automatically converts operands in the following circumstances:

- In **most expressions**: Values of integral types smaller than int are first promoted to larger integral type.
- In **conditions**: Non-bool expressions are converted to bool.
- In **initializations**: Initializer is converted to the type of the variable.
- In **assignments**: Right-hand operand is converted to the type of the left-hand.
- In **arithmetic and relational expressions with operands of mixed types**: Types are converted to a common type.
- **Conversions** also happen during function calls.

**Arithmetic conversions**: Convert one arithmetic type to another. Operands to an operator are converted to the widest type.

- **Integral promotions** convert the small integral types to a larger integral type. Bool, char, signed char, unsigned char, short, unsigned short are promoted to int if all possible values of that type fit in an int. Otherwise, the value is promoted to unsigned int.

- **Larger char types** (wchar_t, char16_t, char32_t) are promoted to the smallest type of int, unsigned int, long, unsigned long, long, long long, unsigned long long in which all possible values of that character type fit.

- If any operand is **unsigned**, the type to which the operands are converted depends on the relative sizes of the integral types on the machine. Integral promotions happen first. Then:

  - If both operands have **same signedness**, the operand with the smaller type is converted to the larger type.
  - If **signedness differs** and the type of the **unsigned operand is the same as or larger** than that of the signed operand, the signed operand is converted to unsigned (example: unsigned int + int > int converted to unsigned int).
  - If **signedness differs** and the type of the **signed operand is larger**, result is machine dependent:

    - If all values in the unsigned type **fit in the larger type**, the unsigned operand is converted to the signed type.
    - If the values **don’t fit**, the signed operand is converted to the unsigned type. Example: long + unsigned int (same size), long is promoted to unsigned int. If long type has more bits, then the unsigned int is converted to long.

```
bool flag;
char cval;
short sval;
unsigned short usval;
int ival;
unsigned int uival;
long lval;
unsigned long ulval;
float fval;
double dval;
3.14L + 'a';    // 'a' promoted to int, then converted to long double
dval + ival;    // ival converted to double
dval + fval;    // fval converted to double
ival = dval;    // dval converted (truncated) to int
flag = dval;    // if dval is 0, flag is false; otherwise true
cval + fval;    // cval promoted to int, then converted to float
sval + cval;    // sval and cval promoted to int
cval + lval;    // cval converted to long
ival + ulval;   // ival converted to unsigned long
usval + ival;   // Conversion depends on the size of unsigned short and int
uival + lval;   // Conversion depends on the size of unsigned int and long
```

The value of a **character constant** (‘a’) depends on the machine’s character set.

**Other implicit conversions**:

- **Array converted to pointer**: In most expressions, an array is automatically converted to a pointer to the first element in that array (example: when we initialize a reference to an array). This conversion is not performed when an array is used with decltype, & (address-of), sizeof or typeid. Similar conversion happes when we use a function type in an expression.

```
int a[10];
int* p = a;    // Converts a to a pointer to the first element
```

- **Pointer conversions**:

  - A constant value of 0 and the literal nullptr can be converted to any pointer type.
  - A pointer to any non-const type can be converted to void*.
  - A pointer to any type can be converted to a const void*.
  - An additional pointer conversion exists that applies to types related by inheritance.

- **Conversion to bool**: Automatic conversion from arithmetic or pointer types to bool. If the pointer or arithmetic value is zero, the conversion yields false; otherwise yields false.

```
char *p = get_string();
if(p) ...                // true if pointer p is not zero
while(*p) ...            // true if *p is not the null character
```

- **Conversion to const**: We can convert a pointer to a non-const type to a pointer to the corresponding const type, and similarly for references.

```
int i;
const int &j = i;       // convert non-const to a reference to const int
const int *p = &i;      // convert address of a non-const to address of a const
int &r = j, *q = p;     // error (conversion from const to non-const not allowed)
```

The reverse conversion (removing a low-level const) doesn’t exists.

- **Conversions defined by class types**: Class types can define conversions that the compiler will apply automatically. The compiler will apply only one class-type conversion at a time.

```
string s, t = "some value";   // character string literal converted to string
while(cin >> s)               // while converts cin to bool
```

### Explicit conversions

Explicitly force an object to be converted to a different type.

```
int i, j;
double slope = i/j;     // We want to explicitly convert i and/or j to double
```

We can use a named cast:

```
cast-name<type> (expression);
```

- __Type__: Target type of the conversion. If type is a reference, the result is an lvalue.
- __Expression__: Value to be cast.
- __Cast-name__: Determines what kind of conversion is performed. May be one of:

  - `static_cast`
  - `const_cast`
  - `reinterpret_cast`
  - `dynamic_cast`

Casts interfere with normal type checking. We recommend to avoid casts. The const_cast can be useful in overloaded functions, but other casts should be needed infrequently.

– `static_cast `:

Any well-defined type conversion, other than those involving low-level `const`, can be requested using a `static_cast`.

```
double slope = static_cast<double>(j) / i;
```

Often useful when a larger arithmetic type is assigned to a smaller type. It turns off compiler warning messages. Also useful to perform a conversion that the compiler will not generate automatically.

```
void* p = &d;                          // Address of any non-const object can be stored in a void*
double *pp = static_cast<double*>(p);  // Converts void* back to the original pointer type
```

We must be certain that the type to which we cast the pointer is the actual type of that pointer; if types don’t match, the result is undefined.

- `const_cast` :

Changes only a low-level const in its operand. Converts a const object to a non-const type (“cast away the const”). Compiler will no longer prevent us from writing to that object. If the object was originally not a const, using a cast to get write access is legal; however, doing so with a const object is undefined. Most useful in the context of overloaded function.

```
const char *p;
char *p = const_cast<char*>(p);   // ok, but writting through p is undefined
```

Only a const_cast may be used to change the constness of an expression. Trying to change this constness with any other named cast is compile-time error. We also cannot use const_cast to change the type of an expression.

- `reinterpret_cast` :

Generally performs a low-level reinterpretation of the bit pattern of its operands.

```
int *p;
char *p2 = reinterpret_cast<char*>(p);
```

You must not forget that the actual object addressed by p2 is an int, not a character. Any use of p2 assuming it’s a char pointer is likely to fail at run-time, but there won’t be any error or warning from the compiler because we explicitly said the conversion was ok.

```
string str(p2);   // Bizarre run-time behavior
```

Any subsequent use of p2 will assume that it holds a char*. Compiler has no way to know that it’s actually an int*. The reinterpret_cast is inherently machine dependent.

- `dynamic_cast` :

Supports run-time type identification.

- Old-style casts :

```
type(expr);     // Function-style cast notation
(type) expr;    // C-language-style cast notation
```

Depending on the types involved, an old-style cast has the same behavior as a `const_cast`, `static_cast` or `reinterpret_cast`. If we use it where a `static_cast` or `const_cast` would be legal, the old-style cast does  that type of conversion. If neither cast is legal, then performs a `reinterpret_cast`.

```
char *p = (char*) a;      // a is int* (same effect as reinterpret_cast)
```


## Compound types

**Compound type**: Type that is defined in terms of another type (references, pointers, etc.).

**Declaration**: Simple declarations are a type followed by a list of names. More generally, a declaration is a **base type** followed by a list of **declarators**.

**Declarator**: Names a variable and gives it a type related to the base type (**type modifier**).

Most known compound types:

- References
- Pointers

A single definition may define variables of different types:

```
int i = 10, *p = &i, &r = i;
```

There are no limits to how many type modifiers can be applied to a declarator.

```
int val = 10;
int *p = &val;
int **pp = &p;
int ***ppp = &pp;
```

```
std::cout << *p;
std::cout << **pp;
std::cout << ***ppp;      // Outputs the value of val
```

### References

**Reference**: Defines an alternative name for an object. A reference type “refers to” another type. References must be initialized. When we define a reference, we bind it to its initializer and there is no way to rebind it to another object later. Two kind of references:

- **lvalue reference**: The regular reference. The topic of this article.
- **rvalue reference**: Special reference primarily intended for use inside classes.

```
int A = 10;
int &refA = A;
int &refA2; // error
```

A reference is not an object, is just another name for an already existing object. That’s why we cannot define a reference to a reference.

```
int B = 10, &refA = A;
int &refB = B, &refC = C;
```

The type of a reference and the referenced object must match exactly (with 2 exceptions: const references to non-const objects, and references to derived classes bound to base class types). A reference can only be bound to an object, not to a literal or a result of a more general expression.

We can define a reference to a pointer:

```
int i = 10;
int *p;
int *&r = p; // Use r the same way you would use p
r = &i;
*r = 5;
```

When __passing arguments by reference__, the reference parameters that are not changed inside a function should be references to const.


### Pointers

Compound type that “points to” another object. Used for indirect access to other objects. It is an object. It can be assigned, copied and can point to different objects over its lifetime. It needs not to be initialized at the time it is defined. Like other built-in types, pointers defined at block scope have undefined value if they are not initialized. Definition:

```
int *A, *B;
double C, *D;     // C is a double
```

A pointer hold the address of another object. We get it using the **address-of operator** (`&`). References are not objects, they don’t have addresses, so we cannot define a pointer to a reference.

```
int val = 10;
int *p1 = &val;
int *p2 = p1;
p2 = p1;
```

Type of the pointer and the object to which it points must match (with 2 exceptions: pointer to const, and pointer in inheritance and polymorphism).

The value stored in a pointer (an address) can be in one of 4 states:

1. Point to an object
2. Point to a location just immediately past the end of an object
3. Be a null pointer (not bound to any object)
4. Be invalid (values other than the previous three)

Cases 2 and 3 don’t point to any object. If we try to access the pointed object, behaviour is undefined. It’s also undefined when trying to access case 4.

To access the pointed object, you can use the **dereference operator** (`*`):

```
*p = 5;             // Assign a new value to the pointed object
std::cout << *p;    // prints 5
int &ref = *p;      // Reference to the (pointed) object
```

In declarations, `&` and `*` are used to form compound types. In expressions are used to denote an operator. Think of them as if they were different symbols.

Ways to obtain a **null pointer**:

```
int *p1 = nullptr;
int *p2 = 0;
int *p3 = NULL;      // requires #include cstdlib
```

`nullptr` is a (pointer) literal that has a special type that can be converted to any other pointer type. “NULL” is a preprocessor variable that `<cstdlib>` defines as 0. Modern C++ programs should avoid `NULL` and use `nullptr`.

**Preprocessor**: Program that runs before the compiler. Preprocessor variables are managed by the preprocessor and are not part of the std namespace. When we use one of its variables, preprocessor automatically replaces the variable by its value.

It is illegal to assign an int variable to a pointer:

```
int zero = 0;
int *p = zero;     // error
```

Recommendation: Initialize all variables. If there is no object to bind, initialize to nullptr or zero so the program can detect that it doesn’t point to an object.

The **assigment** makes the pointer point to a different object.

A pointer can be used in conditions. Any nonzero pointer evaluates as true.

```
if (ptr) {...}
if (p1 == p2) {...}
```

We can use **equality** (`==`) or **inequality** (`!=`) with pointers. Result is bool. Two pointers are equal if they hold the same address (or both are zero), unequal otherwise. Using an invalid pointer in a condition or comparison is undefined.

**`void*` pointers**: It holds an address, but the type of the object at that address is unknown.  Usually, we use it to deal with memory as memory, rather than using it to access the object stored in that memory. We can do a limited number of things with it:

- Compare it to another pointer
- Pass it or return it from a function
- Assign it to another void* pointer
- Cannot use it to operate on the object it addresses

```
double val = 2.72, *pd = &val;
void *pv = &val;
pv = pd;
```


### Pointers to functions

**Function pointer**: Pointer that denotes a function rather than an object. It points to a particular type, which is determined by the return type and types of the parameters of the function.

```
bool length_comp(const string &, const string &);     // Function declaration
bool (*pf)(const string &, const string &);           // Uninitialized pointer to that function
```

When we use the name of a function as a value, the function is automatically converted to a pointer.

```
pf = length_comp;
pf = &length_comp;      // equivalent
```

To call the function through the pointer, there is no need to dereference the pointer. The following calls are equivalent:

```
bool b1 = pf("hello", "bye");
bool b2 = (*pf)("hello", "bye");
bool b3 = length_comp("hello", "bye");
```

There is no conversion between pointers to one function type and pointers to another function type.

We can assign **nullptr** or a **zero-valued integer** constant expression to a function pointer to indicate that the pointer doesn’t point to any function.

```
string::size_type sumLength(const string &, const string &);
bool stringComp(const char*, const char*);
pf = 0; 
pf = sumLength;      // error
pf = stringComp      // error
pf = length_comp;
```

**Pointers to overloaded functions**

The context must make it clear which version is being used.

```
void fun(int *);
void fun(unsigned int);
void (*pf1)(unsigned int) = fun;
void (*pf2)(int) = fun;     // error (no matching parameter type)
double (*pf3)(int*) = fun;  // error (no matching return type)
```

**Function pointer parameters**

Just as with arrays, we cannot define parameters of function type but can have parameters that is a pointer to a function.

```
void getBigger(bool pf(const string &, const string &));
void getBigger(bool (*pf)(const string &, const string &));    // equivalent
```

```
getBigger(length_comp);
```

```
typedef bool func(const string &, const string &);
typedef decltype(length_comp) func2;                     // equivalent
typedef bool(*funcP)(const string &, const string &);
typedef decltype(length_comp) *funcP2;                   // equivalent
```

func and func2 have __function type__. funcP and funcP2 have __pointer to function type__.

```
void getBigger(const string &, const string &, func);
void getBigger(const string &, const string &, funcP2);      // equivalent
```

**Return a pointer to a function**

We cannot return a function type but can return a pointer to a function type. We must write the return type as a pointer type. The easiest way to declare this function is by using a type alias:

```
using F = int(int*, int);       // F is a function type, not a pointer
using PF = int(*)(int*, int);   // PF is a pointer type
```

The return type is not automatically converted to a pointer type. We must explicitly specify that the return type is a pointer type:

```
PF f1(int);   // Ok: PF is a pointer type; f1 returns a pointer to a function
F f1(int);    // Error: F is a function type; f1 cannot return a function
F *f1(int);   // Ok: Explicitly specify that the return type is a pointer to a function
```

We can also declare f1 directly:

```
int(*f1(int))(int*, int);           // read this declaration from inside out
```

We can simplify declarations of functions that return pointer to function by using a trailing return:

```
auto f1(int) -> int (*)(int*, int);
```

**Using auto or decltype for function pointer types**

We can use decltype to simplify writing a function pointer return type.

```
string::size_type sumLength(const string&, const string&);
string::size_type largerLength(const string&, const string&);
decltype(sumLength) *getFcn(const string &);
```

Depending on the values of its string parameter, getFcn returns a pointer to sumLength or to largerLength. We must add `*` to indicate that we are returning a pointer, not a function.


## const qualifier

We make a variable unchangeable by defining the variable’s type as `const`. This variable must be initialized and its value can’t be changed after its creation.

```
const int a = 10;           // initialized at compile time
const int c = get_value()   // initialized at run time
const int;                  // error
a = 10;                     // error
```

When a const is initialized from a compile-time constant, the compiler usually replace uses of the variable with its corresponding value during compilation.

By default, const variables are local to a file. To share a const variable among multiple files, use extern on its definitions and declarations (more about this in the [Extern chapter](#extern)).


### Reference to const

Cannot be used to change the referenced object. A const object can only be referenced by a reference to const. A reference is not an object, so there cannot be const references.

```
const int val = 10;
const int &r1 = val;
r1 = 42;               // error
int &r2 = val;         // error
```

A reference to const may refer to a nonconst object.

```
int i = 10;
const int &r1 = i;      // a ref to const may refer to a nonconst object
const int &r2 = 20;
const int &r3 = r1 * 2;
int &r4 = r1 * 2;       // error
int &r5 = 30; // error
```

We can initialize a reference to const from any expression that can be converted to the type of the reference. We cannot do this with a reference to nonconst.

```
double val = 5.5;
const int &r1 = val;
int &r2 = val;                   // error
std::cout << r1 << " " << val;   // 5  5.5
```

Operations with r1 will be integer operations, but val is a floating-point number. Compiler creates a temporary const int equal to 5 and binds it to r1.

### Pointer to const

Cannot be use to change the pointed object. The address of a const object can only be stored in a pointer to const.

```
const double val = 10;
const double *p1 = &val;
double *p2 = &val;        // error
*p1 = 25;                 // error
```

A pointer to const may point to a nonconst object.

```
double val = 2.5;
const double *p = &val;
```

### const pointer

Must be initialized. Its value (address that holds) cannot be changed. We may use a const pointer to change the pointed object.

```
int num = 0;
int *const p1 = #
*p1 = 3.8;
const double val = 2.5;
const double *const p2 = &val;
*p2 = 3.8;                      // error
```

### Top-level, Low-level const

**Top-level const**: The object itself is const (const pointer).

**Low-level const**:  Appears in the base type of compound types (pointer to const).

When copying an object, **top-level consts** are ignored. Copying an object doesn’t change the copied object.

```
int i = 0;
const int c = 40;
i = c;                     // int = const int
const int *p1 = &c;
const int *const p2 = p1;
p1 = p2;                   // const int* = const int *const
```

When copying an object, **low-level const** is never ignored. Both objects must have the same low-level const or there must be a conversion between both types. In general, we can convert a nonconst to const but not the other way round.

```
int *p = p2;          // error
p1 = p2;
p2 = &i;              // converts int* to const int*
int &r1 = c;          // error
const int &r2 = i;    // binds const int& to int
```

### constexpr and Constant expressions

**constant expression**: Expression whose value cannot change and can be evaluated at compile time. Example:

- literal
- const object initialized from constant expression

Whether a given object or expression is constant expression depends on the types and initializers:

```
const int a = 8;
const int b = a + 1;
int c = 5;               // no constant expression
const int d = func();    // no (initializer isn't known until run time)
```

We can ask the compiler to verify that a variable is a constant expression by declaring the variable in a **constexpr** declaration. Variables declared as constexpr are implicitly const and must be initialized by constant expressions:

```
constexpr int a = 5;
constexpr int b = a + 1;
constexpr int c = func();   // ok only if size() is a constexpr function
```

A constexpr function must be simple enough that the compiler can evaluate it at compile time. You can use constexpr functions in the initializer of a constexpr variable.

**Literal types**: Types we can use in a constexpr (arithmetic, reference, pointer… but no string, library IO…).

You can initialize a **constexpr pointer (or reference)** from literal nullptr or 0, or point (or bind) to an object that remain at a fixed address. Variables defined inside a function often are not stored at fixed addresses, but objects defined outside any function are constant expressions. Functions may define variables that exist across calls to functions (**static** variables), they have fixed addresses too.

constexpr imposes top-level const on the objects it defines. So, when we define a pointer in a constexpr declaration, the constexpr specifier applies to the pointer, not the type to which the pointer points (pointer may point to a const or nonconst type).

```
constexpr int *a = nullptr;
int j = 0;
constexpr int i = 25;
constexpr const int *b = &i;
constexpr int *c = &j;
```

### const parameters and arguments

See [Argument passing](#argument-passing) chapter.

### const variable shared across files

See [Extern](#extern) chapter.

### const: Good practices

`const` is a powerful tool for writing safer code, and it can help compiler optimizations. You should use it.

- **Parameters**:

  - A parameter **passed by value** should not be declared const (it’s useless). Moreover, passing a const pointer (`* const`) is useless.
  - A parameter **passed by reference** should be declared const if it is not modified in the function.

- **Member function**:

  - A **member function** that doesn’t change the state of the object should be declared const.
  - However, if it only modifies the object’s internal state (non-observable, implementation detail), it should be const. The modified variable should be declared `mutable`.

- When using **return-by-value for non-builtin return types**, prefer returning a const value. This makes the compiler emit an error if the caller tries to modify the temporary. Builtin types are already rvalues and declaring them const can interfere with template instantiation.

- **Variables** that never change should be const.

- An `iterator` that doesn’t change the state of the set should be `const_iterator`.

- A const reference (`& const`) is useless (references cannot be changed to refer to a different object).


## Dealing with types

### Type alias

Name that is a synonym for another type. Two ways:

- **typedef**: Put it as part of the base type of a declaration. Declarators can include type modifiers that define compound types built from the base type of the definition.

```
typedef double money;      // now, money is synonym for double
typedef money salary, *p;  // salary  is synonym for money, p for double*
typedef salary d_arr[4];   // d_arr, synonym for array of 4 doubles
```

Declarations using type aliases that represent compound types and const can yield surprising results (base type here is const p):

```
typedef char *p;
const p val1 = 0;        // constant pointer to char
const p *val2;           // pointer to a constant pointer to char
```

- **using**: Alias declaration.

```
using abc = sales;         // abc is synonym for sales (class type)
```

### auto

Let the compiler determine the type of an expression from the initializer by using the **auto** type specifier. Must have an initializer. We can define multiple variables using auto, but their initializers must have types consistent with each other.

```
auto item = a + b;
auto i = 0, *p = &i;
auto c = 0, p = 2.72;    // error
```

When we use a **reference** , we are really using the referenced object, so the compiler uses that object’s type for auto’s type deduction:

```
int i = 0, &r = i;
auto a = r;          // a is an int
```

auto ordinarily ignores **top-level** consts. **Low-level** consts are kept.

```
int i = 0;
const int a = i, &r = a;
auto b = a;             // int
auto c = r;             // int
auto d = &i;            // int*
auto e = &a;            // const int*
```

If we want the deduce type to have **top-level** const, we must say so explicitly:

```
const auto f = a;       // const int
```

If we want a reference to the auto-deduced type:

```
auto &g = a;            // const int&
auto &h = 55;           // error (can't bind plain reference to a literal)
const auto &j = 33;     // literal reference to const
```

```
auto k = a, &l = i;     // int, int&
auto &m = a, *p = &a;   // const int&, const int*
auto &n = i, *p2 = &a;  // error (int, const int*)
```

### decltype

Evaluate an expression an return its type. When the operand is a variable, it return its type, including top-level const and references (decltype is the only context in which a variable defined as a reference is not treated as synonym of the referenced object):

```
decltype(f()) sum = x;
```

```
const int i = 0; &j = i;
decltype(i) x = 0;           // const int
decltype(j) y = x;           // const int&
decltype(j) z;               // error (not initialized)
```

decltype returns a reference type for __expressions__ that yield objects that can stand on the left-hand side of the assignment:

```
int i = 23, *p = &i, &r = i;
decltype(r + 0) b;           // int (the addition yields an int)
decltype(*p) c;              // error (int& must be initialized)
```

decltype(variable), is a reference only if variable is a reference. By enclosing the name of the variable in **parentheses** we make the compiler evaluate the operand as an expression. A variable is an expression that can be left-hand side of an assignment, so on such an expression (`decltype((variable)`) decltype yields a reference.

```
decltype((i)) d;         // error (int& not initialized)
decltype(i) e;           // int
decltype(i = 2) f = i;   // int&
```


## Extern

**Separate compilation**: Split the program into multiple separate source files, each of which can be compiled independently. Store the various parts of the program in separate files and allow programs to be written in logical parts, each of which can be compiled independently.

Let’s assume the definition of `fact()` is in file `fact.cpp`, its declaration is in `fact.h`, and the main function that calls `fact()` is in `factMain.cpp`. We must tell the compiler where to find all the code. We might compile these files as follows:

```
$ CC factMain.cpp fact.cpp           # generates factMain.exe or a.out
$ CC factMain.cpp fact.cpp -o main   # generates main or main.exe
```

- `CC`: Name of our compiler
- `$`: Our system prompt
- `#`: Command-line comment

If we change only one of our source files, most compilers provide a way to separately compile each file, they let us link object files together to form an executable. This process usually yields an `.obj` (Windows) or `.o` (UNIX) file. We can separately compile our programs as follows:

```
$ CC -c factMain.cpp                # generates factMain.o
$ CC -c fact.cpp                    # generates fact.o
$ CC factMain.o fact.o              # generates factMain.exe or a.out
$ CC factMain.o fact.o -o main      # generates main or main.exe
```

Check with your compiler’s user’s guide how to compile and execute programs made up of multiple source files.

We need a way to share code across those files. Example: Code in one file may need to use a variable defined in another file.

To obtain a declaration that is not also a definition, we add the extern keyword and may not provide an explicit initializer.

An extern that has an initializer is a definition. It is an error to provide an initializer on an extern inside a function.

Variables must be defined exactly once but can be declared many times. To use a variable in more than one file requires declarations that are separate from the variable’s definition. To use the same variable in multiple files, we must define that variable in only one of them and declare it in the other files that use it.

### Extern

When you have global variables, you declare the existence of global variables in a header, so that each source file that includes the header knows about it, but you have to define it only once in one of your source files.

Example: Using “extern int A” tells the compiler that an object of type int called A exists somewhere. Compiler doesn’t need to know where, it just needs to know the type and name so it knows how to use it. Once all the source files are compiled, the linker will resolve all of the references of A to the one definition that it finds in one of the compiled source files. To work, the definition of A needs to have “external linkage” (it needs to be declared outside of a function, in the “file scope”), and without the static keyword.

- Header:

```
extern int A;
void printA();
```

- Source 1:

```
#include "header.h"

int A;

int main() {
    A = 3;
    printA();
}
```

- Source 3:

```
#include <iostream>
#include "header.h"

void printA() {
    std::cout << A << std::endl;
}
```

If you declare a global variable in a header file without the extern keyword, each source file that includes that header will have its own variable and each source file will compile independently, but the linker will complain (two source files have the same global identifiers).

### Const

When we split a program into multiple files, every file that uses “const” must have access to its initializer. To see the initializer, the variable must be defined in every file that wants to use the variable’s value. To support this usage, yet avoid multiple definitions of the same variable, **by default, const variables are defined as local to a file**. When we define const variables with same name in multiple files, it is as if we had written definitions for separate variables in each file.

If we have a **const variable that we want to share across multiple files** but whose initializer is not a constant expression, we want the const object to behave like other (nonconst) variables. We define the const in one file and declare it in the other files that use it by using extern on both its definition and declaration.

```
// file1.cc:
extern const int value = func();
// file2.h
extern const int value;
```

### File redirection

Most operating systems support file redirection (associate a named file with the standard input and the standard output). We can write this in the command line:

```
$ myProgram <infile >outfile
```

`$` is the system prompt. `myProgram` is the name of the executable of our compiled program. This command allow to read transactions from file `infile` and write outputs to file `outfile` in the current directory.


## Operators and expressions

### Number of operands

The context determines whether the symbol represents a unary or binary operator.

- **Unary operators** act on 1 operand
- **Binary operators** act on 2 operands
- **Ternary operator** takes 3 operands


### Operand conversions

When an expression is evaluated, operands are often converted from one type to another, so we can use them with differing types so long as the operands can be converted to a common type.

### Overloaded operators

The language defines what the operators mean when applied to built-in and compound types. But we can also define what most operators mean when applied to class types. The meaning of the overloaded operator (including type of its operand/s and result) depend on how the operator is defined. However, the number of operands, precedence and associativity of the operator cannot be changed.

### Lvalues and Rvalues

Every expression in C++ is either an rvalue or lvalue.

- **Lvalue** expressions yields an object or function. When we use an object as an Lvalue, we use the object’s identity (its location in memory).
- When we use an object as **Rvalue** object, we use the object’s value (its contents).

Operators differ as to whether they require lvalue or rvalue operands and as to whether they return lvalues or rvalues. We can (with one exception) use an lvalue when an rvalue is required (the objects’s contents, its value, are used), but we cannot use an rvalue when an lvalue is required. Some operations with lvalues:

- **Assignment** (`=`) requires lvalue as left operand and yields the left operand as lvalue.
- **Address-of operator** (`&`) requires lvalue operand and returns pointer to it as rvalue.
- **Built-in dereference** (`*`) yield lvalue.
- **Built-in subscript** (`[ ]`) yield lvalue.
- **Iterator dereference** (`*`) yield lvalue.
- **String and vector subscript** (`[ ]`) yield lvalue.
- **Built-in iterator increment** (`++`) **and decrement** (`–`) require lvalue. Their prefix versions also yield lvalues.

When applying `decltype` to an expression (other than a variable), the result is a reference type if the expression yields an lvalue. Example: If `p` is an `int*`, because dereference yields an lvalue, `decltype(*p)` is `int&`; and because address-of operator yields an rvalue, `decltype(&p)` is `int**`.

### Precedence and Associativity

Operator precedence-associativity table:

- **Precedence**: How operators are grouped in a compound expression.
- **Associativity**: How operators at the same precedence level are grouped.

Understanding expressions with multiple operators requires understanding the **precedence** and **associativity** of the operators and may depend on the **order of evaluation** of the operands.

**Precedence and Associativity**: Both determine how the operands are grouped in a compound expression. You can override these rules by parenthesizing to force a particular grouping.

- Operands of operators with higher **precedence** group more tightly than operands of operators at lower precedence.
- **Associativity** determines how to group operands with the same precedence.

Arithmetic operators are left associative (operators with same precedence group left to right).

```
3 + 4 * 5       // Yields 23 because of precedence
20-15-3         // Yields 2 because of associativity
6 + 3 * 4 / 2 + 2    // Equivalent to   (6 + ((3 * 4) / 2)) + 2
```

```
int a[] = [0,2,4,6,8};
int last = *(a + 4);      // 8
last = *a + 4;            // 4
```

```
cin >> v1 >> v2;   // IO operators are left associative, so we can combine them
```

<br>![operator_precedence_table](https://raw.githubusercontent.com/AnselmoGPP/Learn_Computer_Science/master/topics/cpp/resources/operator_precedence_table.png)

### Order of evaluation

Precedence specifies how the operands are grouped but says nothing about the order in which the operands are evaluated. In most cases, the order is largely unspecified (to give compiler opportunities for optimization).

```
int i = f1() * f2();    // We cannot know which operand will be called first
```

For operators that don’t specify evaluation order, it is an error for an expression to refer to and change the same object (undefined behaviour).

```
int i = 0;
cout << i << " " << ++i << endl;         // undefined
```

Compiler may evaluate ++i before evaluating i, or viceversa, or something else entirely.

Only **4 operators** guarantee the order of evaluation of operands:

- **AND** (`&&`): Left operand is evaluated first. Right operand is evaluated only if the left one is true.
- **OR** (`||`)
- **Conditional** (`? :`)
- **Comma** (`,`)

Order of operand evaluation is independent of precedence and associativity.

```
f() + g() * h() + j()
```

- __Precedence__ guarantees that results of `g()` and `h()` are multiplied.
- __Associativity__ guarantees that result of `f()` is added to the product `g()h()`, and that result is added to `j()`.
- There are no guarantees as to the order in which these functions are called. This is a problem when these functions affect the state of the same object or perform IO.

**Advice for managing compound expressions**: When writing compound expressions

1. When in doubt, parenthesize expressions to force the grouping.
2. If you change the value of an operand, don’t use that operand elsewhere in the same expression. Exception: When the subexpression that changes the operand is itself the operand of another subexpression (*++iter).

### Operators

- Arithmetic: `+`, `-`, `*`, `/`, `%`
- Logical and Relational operators: `!`, `<`, `<=`, `>`, `>=`, `==`, `!=`, `&&`, `||`
- Assignment operators: `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `<<=`, `>>=`, `&=`, `^=`, `\=`
- Increment and Decrement operators: `++`, `--`
- Member access operators: `.`, `->`
- Conditional operator: `a ? b : c`
- Bitwise operators: `<<`, `>>`, `~`, `&`, `^`, `|`
- sizeof operator: `sizeof`
- Comma operator: `,`

#### Arithmetic

Unary arithmetic operators have higher **precedence** than multiplication/division operator, which in turn have higher precedence than the binary addition and substraction operators. These operators are **left associative** (they group left to right when precedence levels are the same).

<br>![operator_precedence_table](https://raw.githubusercontent.com/AnselmoGPP/Learn_Computer_Science/master/topics/cpp/resources/arithmetic_operators.png)

Unless noted otherwise, the arithmetic operators may be applied to any of the arithmetic types or to any type that can be converted to an arithmetic type. The operands and results of these operators are rvalues. Operands of small integral types are promoted to a larger integral type, and all operands may be converted to a common type as part of evaluating these operators.

Unary minus returns the result of negating the value of its operand. Bool values should not be used for computation. For most operators, operands of type bool are promoted to int. Unary plus, addition and subtraction may also be applied to pointers.

Some arithmetic expressions yield undefined results. Some due to the nature of mathematics (division by zero), others due to nature of computers (overflow: value outside the range of values that the type can represent).

Division between integers returns an integer. If the quotient contains fractional part, it is truncated toward zero.

```
int a2 = 15/5;       // 3
int a1 = 15/4;       // 3 (truncated)
```

**Remainder/Modulus** (`%`): Returns the remainder of a division. Both operands must be integral type.

```
int a = 15;
double b = 2.72;
a % 4;            // 3
a % b;            // error
```

In a division, a nonzero quotient is positive if the operands have same sign, negative otherwise. The quotient is rounded toward zero (truncation).

```
21 / 6           // 3
21 % 6           // 3
21 / 7           // 3
21 % 7           // 0
-21 / -8         // 2
-21 % -8         // -5
21 / -5          // -4
21 % -5          // 1
-21 / 5          // -4
-21 % 5          // -1
```

#### Logical and Relational operators

**Relational operators**: Take operands of arithmetic or pointer type.

**Logical operators**: Take operands of any type that can be converted to bool.

Both return type `bool` values. Operands to these operators are rvalues and the result is rvalue.

<br>![operator_precedence_table](https://raw.githubusercontent.com/AnselmoGPP/Learn_Computer_Science/master/topics/cpp/resources/log_and_rel_operators.png)

**AND** and **OR** always evaluate their left operand before the right. The right is evaluated if and only if the left operand does not determine the result (**short-circuit evaluation**).

- **AND** (`&&`): True only if both operands are true.
- **OR** (`||`): True if either operand is true.
- **NOT** (`!`): Returns inverse of the truth value of its operand.
- `<`, `<=`, `>`, `>=`: Left associative.
- **Equality** (`==`), **Inequality** (`!=`)

```
if(i < j < k)        // mistake (true if 1<k)
if(i < j && j < k)   // Ok
```

```
if(val)          // Test truth value of arithmetic or pointer object
if(!val)         // Compiler converts val to bool. True if val is nonzero
if(val == true)  // If val is not bool, true is converted to val's type. True if val is 1
```

When `bool` is converted to another arithmetic type, `false` converts to 0 and `true` to 1. Literals `true` and `false` should be used only to compare to an object of type `bool`.

#### Assignment operators

Left-hand operand of an assignment operator must be a modifiable **lvalue**.

```
int a = 0, b = 0, c = 0;
const in d = a;           // Ok (initialization, not assignment)
10 = c;                   // error
a + b = c;                // error
d = c;                    // error (d is const lvalue)
```

Result of an assignment is its left-hand operand (an lvalue). Type of the result is the type of left-hand operand. If type of left and right operands differ, the right one is converted to the type of the left.

```
c = 0;       // Result: type: int,  value: 0
c = 2.72;    // Result: type: int,  value: 2
```

We can use a braced initializer list on the right-hand side:

```
c = {2.72};           // error (narrowing conversion)
vector<int> x;        // empty
x = {0,1,2,3,4};      // 5 elements
```

If the left-hand operand is a built-in type, the initializer list may contain at most one value. For class types, what happens depends on details of the class. If initializer list is empty, compiler generates a value-initialized temporary and assigns that value to the left-hand operand.

Assignment is **right associative**.

```
int v1, v2;
v1 = v2 = 0;
```

Each object in a multiple assignment must have the same type as its right-hand neighbor or a type to which that neighbor can be converted.

```
int v1, *v2;
v1 = v2 = 0;     // error
string s1, s2;
s1 = s2 = "Ok";  // string literal converted to string type
```

Assignment has **low precedence** than the relational operators. Parentheses are usually needed around assignments in conditions.

```
int i;
while((i = getValue()) != 30) {...}
```

**Compound assignment operators**: Apply an operator to an object and then assign the result to that same object.

```
Arithmetic operators:     +=   -=   *=   /=   %=
Bitwise operators:       <<=   >>=   &=   ^=   |=
```

Each compound operator is essentially equivalent to: `a = a operator b`.

In a compound assignment, the left-hand operand is evaluated only **once**. If we use an ordinary assignment, that operand is evaluated twice.


#### Increment and Decrement operators

Increment (`++`) and decrement (`--`) operators are a shorthand for adding or subtracting 1 from an object. They require **lvalue** operands. Two forms:

- **Prefix**: Increments (or decrements) its operand and yields the changed object as lvalue.
- **Postfix**: Increment (or decrements) the operand but yield a copy of the original as rvalue. Requires some extra work: has to store original value to return it as result.

```
int i = 0, j;
j = ++i; // j = 1, i = 1
j = i++; // j = 1, i = 2
```

Precedence of postfix increment is higher than that of the dereference operator:

```
auto pbeg = v.begin();
while(pbeg != v.end() && *beg >= 0)
    cout << *pbeg++ << endl;        // *pbeg++  equivalent to  *(pbeg++)
```

```
int a[] = { 1, 2, 3 };
int *p = a;
cout << *p++ << " " << *p;        // Yields:   1   3
```

```
cout << *iter++ << endl;
```

Most operators give no guarantee as to the order in which operands will be evaluated (they can be evaluated in any order). This matters when one subexpression changes the value of an operand that is used in another subexpression. So, pay attention in compound expressions.

```
for(auto i = s.begin(); i != s.end() && !isspace(*i); ++i)
    *it = toupper(*it);
```

```
while(beg != s.end() && !isspace(*beg))
    *beg = toupper(*beg++);             // error (assignment undefined)
```

Problem: Both left and right operands to = use beg and the right operand changes beg. Therefore, the assignment is undefined. Compiler may evaluate it as:

```
*beg = toupper(*beg);
*(beg + 1) = toupper(*beg);
// Or may evaluate it in some other way
```

#### Member access operators

**Dot** and **arrow** operator provide for member access.

- **Dot** (`.`): Fetches a member from an object class type. Yields an lvalue if the object from which the member is fetched is an lvalue; otherwise, result is rvalue.
- **Arrow** (`->`): Defined so that `ptr->mem` is synonym for `(*ptr).mem`. Requires a pointer operand and yields an lvalue.

```
string s = "my string", *p = &s;
auto n = s.size();
n = (*p).size();
n = p->size();
```

Dereference has lower precedence than dot, so we must parenthesize.

```
*p.size();         // error: p is pointer, which has no members
```

#### Conditional operator

**Conditional operator** (`? :`) lets us embed simple `if-else` logic inside an expression.

```
cond ? expr1 : expr2;
```

**cond** is an expression used as a condition. **expr1** and **expr2** are expressions of the same type (or types that can be converted to a common type). If condition is true, expr1 is evaluated; otherwise, expr2 is evaluated.

```
string exam = (grade < 60) ? "fail" : "pass";
```

Only one condition is evaluated. Result is **lvalue** if both expressions are lvalues or they convert to a common lvalue type. Otherwise, is an **rvalue**.

```
exam = (grade > 90) ? "high pass" : (grade < 60) ? "fail" : "pass";
```

Conditional operator is **right associative**. Operands group right to left. **Nested conditionals** quickly become unreadable so nest no more than 2 or 3.

Conditional operator has fairly **low precedence**. When we embed a conditional expression in a larger expression, we usually parenthesize.

```
cout << ( (grade < 60) ? "fail" : "pass" );
 ```

#### Bitwise operators

They are **left associative** and take operands of **integral type** that they use as a collection of bits. Let us test and set individual bits. We can also use these operators on a library type named **bitset** that represents a flexibly sized collection of bits. If an operand is a “small integer”, its value is first promoted to a larger integral type. Operands can be either **signed or unsigned**.

```
<< left shift, >> right shift
~ NOT
& AND
^ XOR
| OR
```

If the operand is **signed** and has negative value, the way the “sign bit” is handled in a number of the bitwise operations is machine dependent. Doing left shift that changes the value of the sign bit is undefined. We recommend using **unsigned** types with the bitwise operators.

We already know the overloaded versions of **`>>` and `<<` operators** defined in the IO library to do input and output. The **built-in** meaning of these operators is that they perform a bitwise shift on their operands. They yield a value that is a copy of the (possibly promoted) left-hand operand with the bits shifted as directed by the right-hand operand. Bits shifted off the end are discarded. The right-hand operand must not be negative and must be a value strictly less than the number of bits in the result; otherwise, the operation is undefined.

Assuming char has 8 bits and int has 32:

```
unsigned char bits = 0233; // Octal literal
bits << 8;                 // bits promoted to int and shifted left 8 bits
bits << 31; bits >> 3;
```

`<<` inserts 0-valued bits on the right. Behaviour of >> depends on the type of the left-hand operand: if unsigned, operator inserts 0-valued bits on the left; if signed, result is implementation defined (either, copies of the sign bit or 0-valued bits are inserted on the left).

**NOT** (`~`) generates a new value with the bits of its operand inverted. Each 1 bit is set to 0; each 0 bit is set to 1.

**AND** (`&`), **OR**(`|`), **XOR**(`^`) generate new values with the bit pattern composed from its 2 operands:

```
unsigned char b1 = 0145; // 01100101
unsigned char b2 = 0257; // 10101111
b1 & b2                  // 00100101
b1 | b2                  // 11101111
b1 ^ b2                  // 11001010
```

**Example**: Each week, the class is given a pass/fail quiz. We can use one bit per student (32 students). To set the bit corresponding to student 27, we generate a value that has only bit 27 turned on:

```
unsigned long quiz1 = 0; // unsigned long has at least 32 bits on any machine
1UL << 27;               // ints are guaranteed to have 16 bits, so we use long int
quiz1 |= 1UL << 27;      // quiz1 = quiz1 | 1UL << 27
```

Generate an integer with only the bit 27 turned off:

```
~(1UL << 27);
quiz1 &= ~(1UL << 27);            //Turn off all the bits except the 27
```

Want to know how the student at position 27 fared:

```
bool status = quiz1 & (1UL << 27);   // True if result is non zeno. False otherwise.
```

An overloaded operator has the same precedence and associativity as the built-in version of that operator. Shift operators are left associative and have midlevel precedence (lower than arithmetic operators but higher than relational, assignment and conditional operators).

```
cout << "hi" << " people" << endl;
cout << 10 + 15;
cout << (10 < 5);
cout << 10 < 5;                   // error
```

**Bitwise operations:**

- Turn certain bit on (`|` + `<<`)
- Turn certain bit off (`&` + `<<` + `~`)
- Check value of a certain bit (& + `<<` + `bool`)
- Shift left or right (`<<`, `>>`)
- Reverse state (`~`)
- XOR (`^`)

```
unsigned long quiz1 = 0; 
quiz1 |= 1UL << 27; // Turn bit 27 on 
quiz1 |= 1UL << 20; // Turn bit 20 on too 
quiz1 &= ~(1UL << 20); // Turn bit 20 off 
bool status27 = quiz1 & (1UL << 27); // Check value at position 27
 ```

#### sizeof operator

Returns the size, in bytes, of an expression or a type name. **Right associative**. Result is a **constant expression** of type **size_t**. Two forms:

```
sizeof (type)
sizeof expr // Returns the size of the type returned by the given expression
```

```
Sales_data dat, *p;
sizeof (Sales_data);
sizeof p; // size of a pointer
sizeof *p; // size of the type p points
sizeof data.revenue; // size of a member (revenue)
sizeof Sales_data::revenue; // size of a member (revenue)
```

Result depends on the type:

- __sizeof char or an expression of type char__: Guaranteed to be 1.
- __sizeof a reference type__: Size of an object of the referenced type.
- __sizeof a pointer__: Size needed to hold a pointer.
- __sizeof a dereferenced pointer__: Size of an object of the type pointed.
- __sizeof an array__: Size of the entire array. Equivalent to taking the sizeof the element type times the number of elements in the array. sizeof doesn’t convert the array to a pointer. So, we can determine the number of elements in an array by dividing the array size by the element size.
- __sizeof a string or a vector__: Size of the fixed part of these types. It doesn’t return the size used by the object’s elements.

Because sizeof returns a constant expression, we can use it to specify the size of an array:

```
constexpr size_t sz = sizeof(ia) / sizeof(*ia);
int arr2[sz];
```

#### Comma operator

Takes **2 operands**, which evaluate **left to right**. Guarantees the order in which its operands are evaluated. Result of a comma expression is the value of its right-hand expression. Result is an lvalue if the right-hand operand is an **lvalue**.

```
vector<int>::size_type cnt = vec.size();
for(vector<int>::size_type x = 0; x != vec.size(); ++x, --cnt)
vec[x] = cnt;
```


## Statements

### Simple statements

Most statements end with **semicolon**. An **expression statement** causes the expression to be evaluated and its result discarded.

```
val + 5;
cout << val;
```

- **Null statements**: Empty statement. Useful where the language requires a statement but the program’s logic does not. They should be commented.

```
;               // null statement
```

```
while(cin >> s && s != sought)
    ;
```

```
val = v1 + v2;; // ok, but superfluous
```

- **Blocks (compound statements)**: Sequence of statements and declarations (possibly empty) surrounded by a pair of curly braces. It is not terminated by a semicolon. A block is a **scope**. Names introduced inside a block are accessible (visible) only in that block and in blocks nested inside that block. An empty block (pair of curlies with no statements) is equivalent to a null statement.

```
while(cin >> s && s != sought)
    { }
```

### Statement scope

We can define variables inside an `if`, `switch`, `while` and `for` statements. They are only visible within that statement.

```
while(int i = get_num()) cout << i << endl;
i = 0;       // error (not accessible)
```

```
auto beg = v.begin();
while(beg != v.end() && *beg >= 0) ++ beg;
if(beg == v.end()) ...
```

### Flow of control

Statements usually execute sequencially, but some flow-of-control statements allow for more complicated execution paths:

- Iteration (loop)                 (Repeats execution until a condition is true)

  - While
  - Do while
  - For
  - Range for

- Selection (condition)       (Executes if a condition is true)

  - If
  - Switch
  - Ternary

- Jump

  - Break
  - Continue
  - Return
  - Goto


### try block and exception handling

See chapter [Exception handling](https://github.com/AnselmoGPP/Learn_Computer_Science/blob/master/topics/cpp/exception_handling.md)


## Keywords, operators and punctuators

















## Keywords

**Reference**: [Keywords](https://en.cppreference.com/w/cpp/keyword)

**Flow of control**:

- `for`: Declares a for-loop or range-based for-loop.
- `do`: Declares a do-while loop
- `while`: Declares a while loop or do-while loop.
- `if`: Conditionally executes another statement.
  - `else`: Declaration of an alternative branch in an if-statement.
- `switch`: Transfers control to one of several statements, depending on the value of a condition.
  - `case`: Label where control can be transferred.
  - `default`: Label where control can be transferred if no previous _case_ label received it.
- `continue`: Skips the remaining portion of the enclosing _for_, _range-for_, _while_, or _do-while_ loop body.
- `break`: Terminates the enclosing _for_, _range-for_, _while_ or _do-while_ loop or _switch_ statement to terminate.
- `goto`: Transfers control unconditionally to another location.
- `return`: Terminates the current function and returns the specified value (if any) to the caller.

**Error handling**: Exceptions and asserts.

- `try`: Specifies a try block.
- `catch`: Catches an exception.
- `throw`: Throws an exception.
- `static_assert`: Performs compile-time assertion checking.

**Types**:

- `auto`: Placeholder type specifier. And other uses.
- `void`: Type with an empty set of values. Objects of type void are disallowed, but pointers to void and functions returning void are permitted.
- `signed`: Target type will have signed representation (this is the default if omitted).
- `unsigned`: Target type will have unsigned representation.
- `int`: Fundamental types. Can be signed (default) or unsigned.
- `short`: Target type will be optimized for space and will have at least 16 bits.
- `long`: Target type will have at least 32 bits.
- `long long`: Target type will have at least 64 bits.
- `float`: Single preision floating-point type (usually, [IEEE-754 binary32](https://en.wikipedia.org/wiki/Single-precision_floating-point_format) format).
- `double`: Double precision floating-point type (usually, [IEEE-754 binary64](https://en.wikipedia.org/wiki/Double-precision_floating-point_format) format).
- `long double`: Extended precision floating-point type (doesn't necessarily map to types mandated by IEEE-754).
- `char`: Character representation. Can be signed or unsigned (the default is implementation defined).
- `wchar_t`: Wide character representation. It holds UTF-32 (32 bits) on Linux and many other systems, but holds UTF-16 (16 bits) on Windows.
- `char8_t`: Unsigned character representing UTF-8 (8 bits).
- `char16_t`: Unsigned character representing UTF-16 (16 bits).
- `char32_t`: Unsigned character representing UTF-32 (32 bits).

**OOP**:

- __Custom types__:
  - `enum`: Declaration of an enumeration type.
  - `struct`: Declaration of a struct type (class public by default).
  - `union`: Declaration of a union type (class that can hold only one of its non-static data members at a time).
  - `class`: Declaration of a class (class private by default), scoped enumeration type, type template parameter, or template template.
  - `template`: Declaration of a template class or function.
- `this`: Used in a member function. Pointer (prvalue) to the object on which the member function is called.
- __Access specifiers__: In a member-specification of a class (a), defines accessibility of subsequent members. In a derived class declaration (b), defines the accessibility of inherited members of the subsequent base class (however, base class private members are always inaccessible to the derived class).
  - `private`: In a, it grants public member access. In b, base class public and protected members keep their member access in the derived class.
  - `protected`: In a, it grants protected member access. In b, base class public and protected members are protected members of the derived class.
  - `public`: In a, it grants public member access. In b, base class public and protected members are private members of the derived class.
- `virtual`: As a function specifier, it specifies that a non-static member function is virtual and supports dynamic dispatch. As a base class specifier, it uses virtual inheritance: in a complex inheritance hierarchy, only one instance of the virtual inherited class is created (example: if both X and Y virtually inherit from A, and another class inherits from both X and Y, only one instance of A will be created).
- `volatile`:
  - As a type qualifier, it indicates that a variable's value can changed at any time by something outside the control of the program (hardware, thread...), preventing the compiler from optimizing code by assuming that the variable's value remains unchanged (prevents caching and disables optimization), ensuring its value is always read from memory (and not cached in a register).
  - As a member function qualifier, it ensures a function is safe to call when the object is volatile. A non-volatile member function cannot be called on a volatile object (compilation error), since the function might assume the object's state won't change and could perform optimizations that aren't safe.
- `typename`: Alternative to class used for declaring type template parameters in a template parameter list of a template declaration.
- `friend`: Declared in a class body for granting a function/class access to private and protected members of that class.
- `operator`: Name of an overloaded operator function, user-defined conversion function, allocation function, deallocation function, or literal operator function.

**Type management**:

- `typedef`: Creates type aliases. Type-safe. Scoped. Doesn't support templates. Less flexible than __using__.
- `using`: Creates type aliases. Type-safe. Scoped. Supports template. More flexible than __typedef__.
- `typeid`: Queries information of a type. Used where the dynamic type of a polymorphic object must be known and for static type identification.
- `decltype`: Type specifier that inspects the type of an expression at compile time and yields that type. 
- `namespace`: Declares or uses a namespace block (prevents name conflicts in large projects), or defines a namespace alias (define an alternate name for a namespace).
- `extern`: Declares a variable/function that is defined in another file (hpp) or translation unit (cpp). It tells the compiler that the definition exists elsewhere and it will be linked during the linking stage of the build process. It also links program units written in different programming languages.
- `inline`: Used to suggest the compiler to replace the function call with the function's body to avoid the overhead of a function call (useful for small, frequently used function). If you define a function inside a header file (which gets included in multiple source files), marking it _inline_ ensures that there won't be multiple definition errors at link time.
- `static`:
  - A static variable declared in a function is initialized once and retains its value across multiple function calls.
  - A static global variable has a scope limited to the file (hpp) or translation unit (cpp) in which it is defined. It's not visible to other files, even if they include that header file.
  - A static data member of a class is shared among all objects of the class. There's only one instance of the static variable regardless of the number of class objects.
  - A static member function of a class can be called without creating an object of the class. It has no access to non-static data members or functions of the class.
- `sizeof`: Queries the size (bytes) of an object or type, or the number of elements in a parameter pack. 
- `alignas`: Explicitly specifies the alignment requirement of a type or an object (so it is stored at a specific byte boundary in memory). 
- `alignof`: Queries alignment requirements of a type or object (number of bytes between successive addresses where the type/object can be stored in memory).

**Constants**:

- `const`:
- `constexpr`:
- `constinit`:
- `consteval`:
- `mutable`:

**Pointers**:

- `new`:
- `delete`:
- `nullptr`:

**Casting**:

- `dynamic_cast`:
- `reinterpret_cast`:
- `static_cast`:
- `const_cast`:

**Comparison**:

- `bool`: Integer type that stores one of two values (true, false).
- `true`: prvalue of type bool.
- `false`: prvalue of type bool.
- `!` (`not`):
- `!=` (`not_eq`):
- `&&` (`and`): 
- `&=` (`and_eq`): 
- `||` (`or`):
- `|=` (`or_eq`):
- `^` (`xor`): 
- `^=` (`xor_eq`): 
- `&` (`bitand`): 
- `|` (`bitor`): 

**Others**:

- `~` (`compl`):
- `concept`:
- `co_await`:
- `co_return`:
- `co_yield`:
- `explicit`:
- `export`:
- `noexcept`:
- `register`:
- `requires`:
- `thread_local`:
- `asm`: Used to declare an inline assembly block.

**Other technical specifications**: TM TS (Transactional Memory Technical Specification) and Reflection TS:

- `atomic_cancel` (TM TS): Atomic block that rolls back on exceptions.
- `atomic_commit` (TM TS): Atomic block that commits on exceptions.
- `atomic_noexcept` (TM TS): Atomic block that aborts on exceptions.
- `synchronized` (TM TS): Synchronized block, executed in single total order with all synchronized blocks.
- `reflexpr` (reflection TS): Get certain data from an enum, a class, or its members.


## Identifiers

They are arbitrarily long sequence of digits, underscores, lowercase and uppercase Latin letters, and most Unicode characters. They can be used to name objects, references, functions, enumerators, types, class members, namespaces, templates, template specializations, parameter packs, goto labels, and other entities. Those containing a double underscore (`__`) in any position, or beginning with an underscore followed by an uppercase letter, are always reserved. Those beginning with an underscore are reserved for use as names in the global namespace. 

**Identifiers** with special meaning:

- `final`: 
- `override`: 
- `transaction_safe`: 
- `transaction_safe_dynamic`: 
- `import`: 
- `module`: 


## Preprocessor directives

- `if`:
- `elif`:
- `else`:
- `endif`:
- `ifdef`:
- `ifndef`:
- `elifdef`:
- `elifndef`:
- `define`: Performs global textual substitution before the code is compiled. Since it's not type-safe, for type aliases prefer __using__ or __typedef__.
- `undef`:
- `include`:
- `line`:
- `error`:
- `warning`:
- `pragma`:
- `defined`:
- `__has_include`:
- `__has_cpp_attribute`:
- `export`:
- `import`:
- `module`:
- `_Pragma`: 


## References

- [Keywords](https://en.cppreference.com/w/cpp/keyword)