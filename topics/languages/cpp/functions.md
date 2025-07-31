# Functions

## Table of Contents
+ [Basics](#basics)
+ [Argument passing](#argument-passing)
+ [Return types and return statement](#return-types-and-return-statement)
+ [Overloaded functions](#overloaded-functions)
+ [Features for specialized uses](#features-for-specialized-uses)


## Basics

**Function**: Block of code with a name. We execute the code by calling the function. May take zero or more **arguments** and, usually, yields a result. It can be **overloaded**. The **parameters** are specified in a comma-separated list enclosed in parentheses.

```
return-type name (parameters) { body }
```

**Call operator ()**: Pair of parentheses used to execute a function. Contains a comma-separated list of arguments used to initialize the function’s parameters.

**Function call**: Initializes the function’s parameters from the arguments and transfers control to that function. Execution of the calling function is suspended and execution of the called function begins. Execution begins with the implicit definition and initialization of its parameters. Ends when a return statement is encountered. Returns the value, if any, and transfers control back to the calling function.

**Arguments**: Initializers for a function’s parameters. Compiler is free to evaluate the arguments in whatever order it prefers. Parameters are always initialized.

```
fact(3.14);         // Parameter is int, so argument is converted to int (truncation)
```

**Parameters**: A function’s parameter list can be empty but cannot be omitted. You may use void to indicate no parameters.

````
int func() { ... }        // Implicit void parameter list
int func(void) { ... }    // Explicit void parameter list
```

No two parameters can have same name. Local variables at the outermost scope of the function may not use the same name as any parameter. Parameter names are optional, but you cannot use an unnamed parameter.

**Return type**: Most types can be used as the return type of a function (it can be void). It may not be an array type or function type, but it may return a pointer to an array or function.

**Local objects**: Names have **scope** (part of the program’s text in which that name is visible). Objects have lifetimes (time during the program’s execution that the object exists). Parameters and variables defined inside a function body are **local variables** (local to the function), and hide declarations of the same name made in an outer scope.

**Global objects**: Objects outside any function exists throughout the program’s execution. They are created when the program exists and are only destroyed when the program ends.

**Automatic object**: Object that exists only while a block is executing. This object is created when the function’s control path passes through the variable’s definition, and destroyed when control reaches the end of the block in which it was defined.

__Parameters__ are automatic objects. They are defined in the scope of the function body and destroyed when function terminates. They are initialized by the arguments passed. Automatic objects corresponding to local variables are initialized if their definition contains an initializer; otherwise, they are default initialized (means undefined values for built-in types).

**Local static object**: Local variable whose lifetime continues across calls to the function. You create it by defining a local variable as static. It is initialized before the first time execution passes through the object’s definition. It’s not destroyed when the function ends, but it is when the program terminates. If it has no explicit initializer, it’s value initialized (means initialized to zero for built-in types).

```
size_t count_calls() {
    static size_t ctr = 0;         // Value persists across calls
    return ++ctr;
}
int main() {                  // Prints numbers from 1 through 10 inclusive
    for(size_t i = 0; i != 10; ++i) cout << count_calls();
    return 0;
}
```

**Function declaration (or function prototype)**: It’s like the function definition, but without function body (semicolon replaces function body). No need for parameters names (often omitted). Like any other name, the name of a function must be declared before we can use it. It may be declared multiple times, but defined only once. The **return type**, **function name** and **parameter types** describe the function’s interface.

```
return-type function-name(parameter-types);
```

Variables and functions should be declared in __header files__ and defined in __source files__. The header that declares a function should be included in the source file that defines that function.

## Argument passing

Parameter initialization works the same way as variable initialization. The type of a parameter determines the interaction between the parameter and its argument.

- If parameter is a **reference**, the parameter is bound to its argument. Arguments are “passed by reference”, function is “called by reference”. Parameter is an alias for its corresponding argument.
- **Otherwise**, the argument’s value is copied. Here, parameter and argument are independent. Arguments are “passed by value”, function is “called by value”.

### Passing arguments by value

The value of the initializer is copied. Changes made to the variable have no effect on the initializer. Nothing the function does to the parameter can affect the argument.

**Pointer parameters**: When we copy a pointer, the value of the pointer is copied. The two pointers are distinct. However, we can change the value of the pointed object.

```
int a = 0, b = 5;
int *p = &a, *q = &b;
*p = 5;                    // a = 5
p = q;                     // p points to I
```

```
void reset(int *p) {
    *p = 0;        // value or pointed object changes
     p = 0;        // changes the local copy of p. Argument unchanged.
}
```

### Passing arguments by reference

Operations on a reference are operations on the object to which the reference refers. Reference parameters allow a function to change the value of one or more of its arguments.

```
void reset(int &i) {
    i = 0;
}
```

We pass an object directly, theres is no need to pass its address:

```
int j = 30;
reset(j);           // value in j is changed
```

It can be inefficient to copy objects of large class types or large containers; and some class types (like IO types) cannot be copied. Functions must use reference parameters to operate on objects of a type that cannot be copied.

```
bool isShorter(const string &s1, const string &s2) {
    return s1.size() < s2.size();
}
```

Reference parameters that are **not changed** inside a function should be references to const.

A function can **return** only a single value. Reference parameters let us return multiple results.

```
string::size_type find_char(const string &s, char c, string::size_type &occurs) {
    auto ret = s.size();
    occurs = 0;
    for(decltype(ret) i = 0; i != s.size(); ++i) {
        if(s[i] == c) {
            if(ret == s.size()) ret = i;
            ++occurs;
        }
    }
    return ret;     // count is returned implicitly in occurs
}
```

```
auto index = find_char(s, 'o', ctr);
```

- ctr: Number of times o occurs.
- index = First occurrence if there is one.

### const parameters and arguments

Top-level const applies to the object itself. When we copy an argument to initialize a parameter, top-level consts are ignored (the same in top-level const parameters). We can call abc passing a const int or plain int.

```
void abc(const int a);       // abc can read but not write to a
```

We can define several functions with same name only if their parameter lists are sufficiently different. Because top-level consts are ignored, we can pass exactly the same types to either of the following versions:

```
void abc(const int a);
void abc(int a);                // error: Redefines abc(int)
```

Parameters are initialized in the same way that variables. We can initialize an object with a low-level const from a non-const object but not vice versa, and a plain reference must be initialized from an object of the same type.

```
int i = 30;
const int *cp = &i;    // cp cannot change i
const int &r1 = i;      // r1 cannot change i
const int &r2 = 25;
int *p = cp;            // error
int &r3 = r;            // error
int &r4 = 15;           // error
```

```
void reset(int*);
void reset(int&);
string::size_type find_char(const string &s);
-----------------------------------------------
int i = 0;
const int ci = i;
string::size_type ctr = 0;
reset(&i);               // calls reset(int*)
reset(&ci);              // error (cannot initialize int* from const int*)
reset(i);                // calls reset(int&)
reset(ci);               // error (cannot bind plain reference to const object)
reset(35);               // error (cannot bind plain reference to a literal)
reset(ctr);              // error (types don't match: ctr is unsigned)
find_char("Hello world");   // ok (first parameter is reference to const)
```

We can call reset(int&) only on int objets. We cannot pass a literal, an expression that evaluates to an int, an object that requires conversion, or a const int object. We may pass only an int* to reset(int*). We can pass a string literal to find_char(const string&).

Use **reference to const** when possible. It’s a mistake to define a parameter as **plain reference** when the function doesn’t change it. It limits the type of valid arguments (cannot pass a const object, literal or an object that requires conversion to a plain reference).

### Array parameters

We cannot copy an array. When we use an array, it’s usually converted to a pointer. Because we cannot copy an array, we cannot pass an array by value. When we pass it to a function, we actually pass a pointer to the array’s first element.

The following declarations are equivalent:

```
void print(const int*);
void print(const int[]);
void print(const int[10]);   // dimension for documentation purposes (at best)
```

Here, compiler only checks that the argument has type `const int*`:

```
int i = 0, j[2] = {0, 1};
print (&i);                   // &i is int*
print(j);                     // j converted to int* that points to j[0]
```

Size of the array is irrelevant. Ensure that all uses of the array stay within the array bounds. Functions ordinarily don’t know the size of the array they are given. They must rely on additional information provided by the caller. Three common techniques to manage pointer parameters:

- **Using a marker to specify the extent of an array**:

The array itself contains an end marker. C-style strings are character arrays where the last character of the string is followed by a null character. Functions that deal with C-style strings stop processing the array when they see a null character.

```
void print(const char *p) {
    if(p)                        // if p is not a null pointer
        while(*p)                // so long the pointer character is not a null character
            cout << *p++;
}
```

Works well for data where there is an obvious end-marker value (like the null character). Works less well with data (such as ints) where every value in the range is a legitimate value.

- **Using the Standard Library conventions**:

Pass pointers to the first and one past the last element in the array. Here, the library functions begin() and end() provide those pointers.

```
void print(const int *beg, const int *end) {
    while(beg != end)
        cout << *beg++ << endl;
}
```

```
int j[2] = {0, 1};
print(begin(j), end(j));
```

- **Explicitly passing a size parameter**:

Define a second parameter that indicates the size of the array.

```
void print(const int a[], size_t size) {
    for(size_t i = 0; i != size; ++i) {
        cout << a[i] << endl;
    }
}
```

```
int j[] = {0, 1};
print(j, end(j) - begin(j));
```

**Array parameters and const**:

When a function does not need write access to the array elements, the array parameter should be a pointer to const. It should be a plain pointer to non-const only if the function needs to change element values.

**Array reference parameters**:

We can define a parameter that is a reference to an array. We can only call the following function `print()` with an array of exactly 10 ints:

```
void print(int (&arr)[10]) {
    for(auto elem : arr) cout << elem << endl;
}
```

```
int i = 0, j[2] = {0, 1};
int k[10] = {0,1,2,3,4,5,6,7,8,9,0};
print(&i);           // error
print(j);            // error
print(k);            // ok
```

Parentheses around `&arr` are necessary:

```
f(int &arr[10])        // error (array of references)
f(int (&arr)[10])      // ok (reference to array)
```

**Passing multidimensional array**:

There are no multidimensional arrays in C++, just arrays of arrays. As with any array, it is passed as a pointer to its first element. The size of the second dimension (and any subsequent) is part of the element type and must be specified.

- Example 1 (parameter is a pointer to array):

```
void print(int (*matrix)[10], int rowSize) {...}
```

Parentheses around `*matrix` are necessary:

```
int *matrix[10];      // array of 10 pointers
int (*matrix)[10];    // pointer to an array of 10 ints
```

We can also define our function using array syntax. Compiler ignores the first dimension, so it’s best not to include it.

- Example 2 (parameter is pointer to array):

```
void print(int matrix[][10], int rowSize) { }  // pointer to array of 10 ints
```

- Example 3 (parameter is pointer to a pointer):

```
void print(int **matrix) {...}
```

```
int **array;
array = new int *[10];
for(int i=0; i<10; i++) array[i] = new int[15];
print(array);
```

### main: Handling command-line options

Sometimes we need to pass arguments to main (usually to let the user specify some options). With the command-line we can pass 2 (optional) parameters:

```
int main(int argc, char *argv[]) {..}
```

- **argv**: Array of pointers to C-style character strings.
- **argc**: Number of strings in that array

Because the second parameter is an array, we might alternatively define main as:

```
int main(int argc, char **argv) {...}     // argv points to char*
```

When arguments are passed to main, the first element in argv points either to the name of the program or to the empty string (so, optional arguments begin in argv[1]). Subsequent elements pass the arguments provided on the command line. The element just past the last pointer is guaranteed to be 0.

We can call the function in the command-line:

```
program_name -d -o ofile data0
```

```
argv[0] = "program_name";       // or point to an empty string
argv[1] = "-d";
argv[2] = "-o";
argv[3] = "ofile";
argv[4] = "data0";
argv[5] = 0;
```

### Functions with varying parameters

Sometimes we don’t know in advance how many arguments we need to pass to a function. The standards provide 2 primary ways to make it:

- **Same type arguments**: Pass _initializer_list__ library type.
- **Varying type arguments**: Write a __variadic template__ (special kind of function).
- **Varying type arguments**: Pass an __ellipsis__ (special parameter type). Should be used only in programs that needs to interface to C function.

#### initializer_list parameters

Library type (template type) that represents an array of values of the specified type. Defined in the `<initializer_list>` header. Operations supported:

```
initializer_list<T> list;           // Default init. Empty list of elements of type T
initializer_list<T> list{a,b,c...}; // As many elements as initializers
list2(list);    // Copying or assigning an initializer_list doesn't copy,...
list2 = list;   // ... just the original and the copy share the elements.
list.size();    // Number of elements
list.begin();   // Pointer to first element
list.end();     // Pointer to one past the last element
```

Elements in an `initializer_list` are always `const` values, there is no way to change them. The values passed to an `initializer_list` parameter must be enclosed in curly braces.

```
void message(ErrCode err, initializer_list<string> abc) {
    if(err.type() == 0) return;
    for(auto beg = abc.begin(); beg != abc.end(); ++beg) 
        cout << *beg << " ";
}
```

```
if(expected != actual) message(err(1), {"functionX", expected, actual});
else message(err(0), {"functionX", "okay"});       // expected and actual are strings
```

Because `initializer_list` has begin and end members we can use a **range for** to process the elements.

```
for(string a : abc) …
```

#### Ellipsis parameters

They are in C++ to allow programs to interface to C code that uses varargs (C library facility). It should not be used for other purposes. Your C compiler documentation describes how to use varags.

Should be used only for types common to both C and C++. Objects of most class types are not copied properly when passed to an ellipsis parameter.

It may appear only as the last element in a parameter list. It may take either  of 2 forms:

```
void foo(parm_list, ...);
void foo(...);
```

The first form specifies the type(s) for some of foo’s parameters. Arguments that correspond to the specified parameters are type checked as usual. No type checking is done for the arguments that correspond to the ellipsis parameter. In this form, the comma following the parameter declaration is optional.


## Return types and return statement

The return statement terminates the function that is currenty executing and returns control to the point from which the function was called. Two forms:

```
return;
return expression;
```

### Functions with no return value

A return with no value may be used only in a function that returns void, although it doesn’t require to contain a return. It’s usually used to exit the function in an intermediate point. It may return the result of another function that returns void.

### Functions that return a value

Every return in a function with a return type other than void must return a value, and it must be the same type as the function return type or a type that can be implicitly converted.

Values are returned in exactly the same way as variables and parameters are initialized: The return value (result of the function call) is used to initialize a temporary at the call site.

Remember the initialization rules in functions that return local variables. Examples of return types:

- `string`: The returned value is copied to the call site.
- `const string &`: The returned value is not copied.

Never return local objects or pointer to local objects.

#### Functions that return class types

The call operator `()` has associativity and precedence (same precedence as dot and arrow operators and left associative like them). If a function returns a pointer, reference of object of class type, we can use the result of a call to call a member of the resulting object.

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

A function with a return type other than void must return a value. However, `main()` is an exception because when control reaches the end of `main()` and there is no return, then the compiler implicitly inserts a return of 0.

A value returned from main() is trated as a status indicator (0 is success, other values are failure). A nonzero value has machine dependent meaning. To make return values machine independent, `<cstdlib>` defines 2 preprocessor variables that can be used to indicate success or failure:

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
```


## Overloaded functions

Functions that have the same name but different parameter lists and that appear in the same scope. They must differ in the number or the type/s of their parameters. Compiler can deduce which function we want based on the argument type we pass. We should only overload operations that actually do similar things. main() may not be overloaded.

### const parameters

Top-level const has no effect on the objects that can be passed to the function. A parameter that has a top-level const is indistinguishable from one without a top-level const.

```
int record(phone);
int record(const phone);     // Redeclared
int record(phone*);
int record(phone* const);    // Redeclared
```

We can overload base on whether the parameter is a reference (or pointer) to the const or non-const version of a given type (such consts are low-level):

```
int record(account&);
int record(const account&);          // reference to const
int record(account*);
int record(const account*);          // pointer to const
```

Because there is no conversion from const, we can pass a const object (or pointer to const) only to the version with a const parameter. Because there is a conversion to const, we can call either function on a non-const object or a pointer to non-const. Compiler will prefer the non-const versions when we pass a non-const object or pointer to non-const.

### const_cast

const_casts are most useful in the context of overloaded functions.

```
const string &shorterString(const string &s1, const string &s2) {
     return s1.size() <= s2.size() ? s1 : s2;
}
```

This function takes and returns references to const string. We can call the function on a pair of non-const string arguments, but we’ll get a reference to a const string as the result.

```
string &shorterString(string &s1, string &s2) {
     auto &r = shorterString(const_cast<const string&>(s1),
               const_cast<const string&>(s2));
     return const_cast<string&>(r);
}
```

This version, when given non-const arguments, would yield a plain reference. It calls the const version of the function by casting its arguments to references to const. It returns a reference to a const string. It’s safe to cast that string back to a plain string& in the return.

### Calling an overloaded function

**Function matching (or overload resolution)**: Process by which a particular function call is associated with a specific function from a set of overloaded functions. The compiler determines which function to call by comparing the arguments in the call with the parameters offered by each function in the overload set.

For any given call to an overloaded function, there are 3 possible outcomes:

- **Match**: Compiler finds exactly one function that is a best match.
- **No match**: There’s no function with parameters that match (error).
- **Ambiguous call**: More than one function matches (error):

### Overloading and scope

Ordinarilly, it’s a bad idea to declare a function locally. If we declare a name in an inner scope, that name hides uses of that name declared in an outer scope. Names don’t overload across scopes.

```
string read();
void print(const string &);
void print(double);
void foo(int ival) {
    bool read = false;      // hides outer "read"
    string s = read();      // error: read is a bool, not a function
    void print(int);        // hides previous instances of print
    print("Value: ");       // error: print(const string &) is hidden
    print(ival);
    print(3.14);
}
```

In C++, name lookup happens before type checking.

### Function matching

1. It identifies the set of overloaded functions considered for the call (**candidate functions**: functions with the __same name__ as the called function and visible at the point of the call).

2. Selects from the set of candidate functions those functions that can be called with the arguments in the given call (**viable functions**: those with the __same number of parameters__ as there are arguments, and the types must __match or be convertible__).

3. It determines, argument by argument, which viable function provides the **best match** for the call. The __closer the types__ of the argument and parameter, the better. An exact match is better than a match that requires conversion. The overall best match is the one, and only one function, for which:

  a. Each argument is no worse than the match required by any other viable function
  b. There is at least one argument for which the match is better than the match provided by any other viable function.

If there is no single function that is preferable, the call is an error (ambiguous call). To determine the best match, the compiler ranks the conversions as:

1. **Exact match**: Argument and parameter types are identical – Argument is converted from an array or function type to the corresponding pointer type – A top-level const is added to or discarded from the argument.
2. Match through a const conversion.
3. Match through a promotion.
4. Match through an arithmetic or pointer conversion.
5. Match through a class-type conversion.

In a call, small integral types always promote to int or larger integral type. Given 2 functions, one of which takes an int and the other a short, the sort version will be called only on values of type short. Smaller integral values are promoted to int. Calling the short version requires a conversion.

```
void func(int);
void func(short);
func('a');              // char promotes to int
```

All the arithmetic conversions are treated as equivalent to each other, it doesn’t take precedence.

```
void manip(long);
void manip(float);
manip(3.14);                     // error: ambiguious call
```

**const arguments**: When we call an overloaded function that differs on whether a reference or pointer parameter refers or points to const, the compiler uses the “constness” of the argument to decide which function to call.

```
record lookup(account &);
record lookup(const account &);
const account a;
account b;
lookup(a);          // lookup(const account &)
lookup(b);          // lookup(account &)
```

For object a, the only viable function is the version that takes a reference to const. For object b, both functions are viable. However, initializing a reference to const from a non-const object requires a conversion. For b, the version that takes a non-const parameter is an exact match.

**Pointer parameters** are similar. If the argument is a pointer to const, the call will match the function that takes a `const*`; otherwise, if the argument is a pointer to non-const, the function taking a plain pointer is called.

**Casts** should not be needed to call an overloaded function. The need for a cast suggests that the parameter sets are designed poorly.

### Overloading member functions

Member functions may be overloaded as long as the functions differ by the number and/or types of parameters. The function-matching process is the same as for nonmember functions.


## Features for specialized uses

### Default arguments

Functions with default arguments can be called with or without that argument. If a parameter has a default argument, all the parameters that follow it must also have default arguments. Default arguments are used for the right-most arguments of a call. To use the default argument, omit that argument when you call that function.

```
void dimensions(int a; double b = 3.14, float c = 137);
dimensions(42, 1.41);        // a = 42,  b = 1.41,  c = 137
```

It’s legar to redeclare a function multiple times. However, each parameter can have its default specified only once in a given scope. Subsequent declarations can add a default only for a parameter that has not previously had a default specified.

```
std::string dimensions(int, int, char = 'A');
std::string dimensions(int, int, char = 'B');     // error: redeclaration
std::string dimensions(int = 1, int = 2, char);   // ok
```

Default arguments ordinarily should be specified with the function declaration in an appropriate header.

Default arguments can be any expression that has a type that is convertible to the type of the parameter. Local variables may not be used as a default argument.

Names used as default arguments are resolved in the scope of the function declaration (so, default arguments cannot be hidden in inner scopes for the function call). The value that those names represent is evaluated at the time of the call.

```
int a = 25;
char c = 'A';
int dim();
double sizes(int = a, int = dim(), char = c);
void func() {
    int a = 100;
    c = 'B';
    double wall = sizes();    // sizes(25, dim(), 'B')
}
```

### Calling a function for each operation

**Advantages:**

- Easier to read
- Easier to change
- Can be reused
- Uniform behaviour

**Disadvantage:**

Calling a function is apt to be slower than evaluating the equivalent expression. A function call does a lot of work:

- Registers are saved before the call and restored after the return
- Arguments may be copied
- The program branches to a new location

### Inline functions

Avoids function call overhead because they are (usually) expanded “in line” at each call. Define an inline function by putting the keyword “inline” before the function’s return type. The inline specification is only a request to the compiler (it may choose to ignore it). The inline mechanism is meant to optimize small, straight-line functions that are called frequently. Many compilers will not inline a recursive function. A 75-line function will almost surely not be expanded inline.

### constexpr function

Function that can be used in a constant expression. Defined like any other function but must meet certain restrictions:

- Return type and type of each parameter must be a literal type.
- Function body must contain exactly one return statement.

```
constexpr int form() { return 42; }
constexpr int value = form();
```

Compiler can verify, at compile time, that a call to form() returns a constant expression. Compiler will replace a call to a constexpr function with its resulting value. constexpr functions are implicitly inline.

A constexpr function body may contain other statements so long as those statements generate no actions at run time (examples: null statements, type aliases, using declarations). It may return a value that is not constant.

```
constexpr size_t scale(size_t cnt) { return new_sz() * cnt; }
int arr[scale(2)];    // scale(2) is a constant expression
int i = 2;            // i is not a constant expression
int a2[scale(i)];     // error: scale isn't a constant expression
```

The scale() function will return a constant expression if its argument is a constant expression, but not otherwise. When we passa constant expression (such as 2), the return is a constant expression. If we pass a non-constant expression, the return is not a constant expression. If we use scale() in a context that requires a constant expression, the compiler checks that the result is a constant expression. If it is not, compiler will produce an error message.

**inline** and **constexpr** functions normally are defined in headers.
