# Classes

## Table of Contents
+ [Introduction](#introduction)
+ [Definition](#definition)
+ [Member functions](#member-functions)
+ [Access control and encapsulation](#access-control-and-encapsulation)
+ [Additional class features](#additional-class-features)
+ [Class scope](#class-scope)


## Introduction

We use **classes** to define our own **data types**. This makes our programs easier to write, debug and modify. Classes are based on:

- **Data abstraction**: Technique that relies on the __separation__ of interface and implementation.
- **Encapsulation**: To __hide__ the implementation, so users can only use the interface.

A class that uses data abstraction and encapsulation defines an **abstract data type**. When designing a class, we should think about how easy it will be to use the class. When we use it, we shouldn’t think about how the class works. A well designed class has an intuitive and easy to use interface, and an efficient implementation.

**User**: It doesn’t have to be the ultimate user of the application, it can be another programmer.

```
class myClass {
   member1;
   member2();
public:
   member3;
   member4();
}
```

**Data structure**: Way to group together related data elements and a strategy for using those data. We define our own data types by defining a class.

We define our own data structures by defining a class. It defines a type (storage requirements and operations related to it), making possible to define class types that behave as naturally as the built-in types. Class defines what happens when an object is created.

## Definition

Classes are usually defined in a **header file**. Ordinarily, we call a member function on behalf of an object. Dot operator applies only to objects of class type. Result: the member named at the right.

```
object_1.data_member;
object_1.member_function();
```

Names defined inside a class must be unique within the class but can reuse names defined outside the class. The close curly that ends the class must be followed by a semicolon. We can define variables outside the class body. Two ways to define objects:

```
struct MyClass { ... } item1, item2, *ptr;
```

```
MyClass item1, item2, *ptr;
```

We can supply an **in-class initializer** for a data member by inclosing it inside curly braces or follow an `=` sign.

## Member functions

**Member functions** must be declared inside the class. May be defined inside or outside the class body. Nonmember functions that are part of the interface are declared and defined outside the class. Functions defined in the class are implicitly **inline**.

With one exception, when we call a member function (use dot operator), we do so on behalf of an object.

### this

Member functions access the object on which they were called through an extra, implicit parameter named **this**. When we call a member function, this is initialized with address of the object on which the function was invoked.

```
obj.m_func()         // pseudo-code:  myclass::m_func(&obj)
```

Compiler passes the address of obj to the implicit this parameter in `m_func()`. Inside a function, we can refer directly to the members of the object on which the function was called. Any direct use of a member of the class is assumed to be an implicit reference through this (as if we had written `this->m_func`).

Parameter this is defined for us implicitly. It’s illegal for us to define a parameter of a variable named this. Inside of the body of a member function, we can use this. It is a const pointer, so we cannot change the address this holds.

**Funtions that return *this**

```
inline Screen &Screen::set(pos r, pos col, char ch) {
    // ...
    return *this
}
```

A member may return a **reference** to the object on which it is called. Functions that return a reference are lvalues, which means that they return the object itself, not a copy. This allows expressions like:

```
myScreen.move(4,0).set('#');       // these operation execute on the same object
```

If the function had a **non-reference** return type, then the return value would be a copy of `*this` (the contents of myScreen will be unchanged).

- **Returning *this from a const member function**

If display is a **const** member, then this is a pointer to const and `*this` is a const object. Hence, the return type of display must be `const sales&`. However, if display returns a const reference, the call to set is an error.

```
Screen myScreen;
myScreen.display(cout).set('*');
```

Even though `myScreen` is a non-const object, the call to set won’t compile because the const version of `display` returns a reference to const and we cannot call set on a const object.

A const member function that returns `*this` as a reference should have a return type that is a reference to const.

- **Overloading based on const**

We can overload a member function based on whether it is const for the same reasons that we can overload a function based on whether a pointer parameter points to const. The non-const version will not be viable for const objects; we can only call const member functions on a const object. We can call either version on a non-const object, but the non-const version will be a better match.

```
class Screen {
public:
    Screen &display(std::ostream &os) {
        do_display(os); 
        return *this;
    }
    const Screen display(std::ostream &os) const {
        do_display(os);
        return *this;
    }
private:
    void do_display(std::ostream &os) const {
        os << contents;
    }
};
```

As always, when one member calls another, the this pointer is passed implicitly. Thus, when display calls `do_display`, its own this pointer is implicitly passed to `do_display`. When the non-const version of display calls `do_display`, its this pointer is implicitly converted from a pointer to non-const to a pointer to const.

The display functions each return the object on which they execute by dereferencing this. The non-const version returns an ordinary (non-const) reference; the const member returns a reference to const.

When we call display on an object, whether that object is const determines which version of display is called.

```
Screen myScreen(5,3);
const Screen blank(5,3);
myScreen.set('#').display(cout);      // calls non-const version
blank.display(cout);                  // calls const version
```

### const member functions

The keyword const following the parameter list modifies the type of the implicit this pointer.

By default, this is a const pointer to the non-const version of the class type (myclass *const). So, by default, we cannot bind this to a const object, which means we cannot call an ordinary member function on a const object. A const following the parameter list indicates that this is a pointer to const. Member functions that use const in this way are const member functions. __Const member functions cannot change the object on which they are called__.

Objects that are const, and references or pointers to const objects, may call only const member functions.

### Scope

A class is itself a scope. The definitions of the member functions of a class are nested inside the scope of the class itself.

The compiler compiles first the member declarations and then the member function bodies. Thus, member function bodies may use other members of their class regardless of where in the class those members appear.

**Defining a member function outside the class**: The return type, parameter list, and name must match the declaration in the class body. The member’s name must include the name of its class. If the member was declared as a const member function, the definition must specify const after the parameter list.

```
double myClass::mem_func() const {
    // ...
}
```

The **scope operator** (`::`) is used to say that mem_func() is declared in the scope of myClass.

**Defining a function to return “this” object**:

```
Sales& Sales::combine(const Sales &obj) {
    units_sold += obj.units_sold;
    revenue += obj.revenue;
    return *this;
}
```

Add the members of obj into the members of “this” object and return the dereferenced object on which the function was called. We don’t need to use the implicit this pointer to access the members of the object on which a member function is executing, but we do need to use this to access the object as a whole.

```
total.combine(sales_obj);      // Update the running total
```

To return an **lvalue**, `combine()` must return a **reference**.

### Defining nonmember class-related functions

Auxiliary functions define operations that are conceptually part of the interface of the class, but they are not part of the class itself. Define them as any other function. It’s typically declared (but not defined) in the same header as the class.

```
istream &read(istream &is, Sales &item){
    double price = 0;
    is >> item.book_num >> item.units_sold >> price;
    item.revenue = price * item.units.sold;
    return is;
}

ostream &print(ostream &os, const Sales &item){
    os << item.isbn() << " " << item.units_sold << " " << item.revenue << " " item.avg_price();
    return os;
}
```

`read()` reads data from the given stream into the given object. `print()` prints the contents of the given object on the given stream (ordinarily, functions that do output should do minimal formatting). The IO classes are types that cannot be copied, so we may only pass them by reference. Reading or writing to a stream changes that stream, so both functions take ordinary references, not references to `const`.

```
Sales add(const Sales &objA, const Sales &objB){
    Sales sum = objA;
    sum.combine(objB);
    return sum;
}
```

`add()` takes 2 Sales objects and returns a new `Sales` representing their sum.

### Constructors

Classes control **object initialization** by defining one or more special member functions (constructors). They initialize the **data members** of a class object. It’s run whenever an object of a class type is created. They have the same name as the class but no return type. A class can have **multiple** constructors, but they must differ from each other in the number or types of their parameters. They may not be declared as **const**. They can write to **const objects** during their construction.

**Synthesized default constructor**:

Compiler-generated constructor used by classes to control default initialization. It takes no arguments. It’s defined (implicitly) only if our class doesn’t explicitly define any other constructor. For most classes, it initializes each data member as follows:

- If there is an in-class initializer, use it to initialize the member
- Otherwise, default-initialize the member

If we define any constructors, the class will not have a default constructor unless we define that constructor ourselves.

For some classes, the default constructor does the wrong thing. Remember that objects of __built-in or compound type__ (arrays, pointers…) __defined inside a block have undefined value__ when they are default initialized. The same rule applies to members of built-in or compound type that are default initialized. __Initialize them inside the class or define your own default constructor__; otherwise, users could create objects with members that have undefined value.

Sometimes the compiler is unable to synthesize one. Example: a class has a member that has a class type that doesn’t have a default constructor. Here, the compiler can’t initialize that member.

```
struct Sales {
   Sales() = default;
   Sales(const std::string &s): book_num(s) { }
   Sales(const std::string &s, usigned n, double p)
: book_num(s), units_sold(n), revenue(p*n) { }

   Sales(std::istream &);

   std::string isbn() const { return book_num;}
   Sales& combine(const Sales&);
   double avg_price() const;
   std::string book_num;
   unsigned units_sold = 0;
   double revenue = 0.0;
};
```

```
Sales() = default;
```

`= default` asks the compiler to generate the default constructor. This constructor does exactly the same as the synthesized default constructor. The `= default` can appear with the declaration inside the class body or on the definition outside the class body.

The **default constructor is used** automatically whenever an object is default or value initialized. Default initialization happens when:

- we define non-static variables or arrays at block scope without initializers
- a class that itself has members of class type uses the synthesized default constructor
- members of class type aren’t explicitly initialized in a constructor initializer list

**Value initialization** happens:

- During array initialization when we provide fewer initializers than the size of the array
- When we define a local static object without an initializer
- When we explicitly request value initialization by writing an expression of the form `T()` where T is the name of a type.

Classes must have a default contructor in order to be used in these contexts. It’s almost always right to provide a default constructor if other constructors are being defined.

```
class NoDefault {
public:
    NoDefault(cont std::string&);
};

struct A {
    NoDefault my_mem;
};

A a;                 // Error: cannot synthesize a constructor for A
struct B {
    B() {}           // Error: no initializer for b_member
    NoDefault b_member;
};
```

**Implicit class-type conversions**: A constructor that can be called with a single argument defines an implicit conversion from the constructor’s parameter type to the class type (converting constructor).

```
class Sales {
public:
    //...
    Sales(const std::string &s) : bookNo(s) { }
    Sales(std::istream&);
    Sales &combine(const Sales);
    std::string bookNo;
}

string null_book = "9-999-99999-9";
item.combine(null_book);
item.combine(cin);
```

The `Sales` constructors that takes a string or a istream define implicit conversions from those types to Sales. We can use a string where an object of type Sales is expected. Here, we call `combine()` with a string argument and the compiler automatically creates a Sales object from the given string. Because `combine()`‘s parameter is a reference to const, we can pass a temporary to that parameter.

**Only one class-type conversion is allowed**: Compiler will automatically appliy only one class-type conversion.

```
item.combine("9-999-99999-9");     // Wrong: Requires converting parameter to string and then the string to Sales
item.combine(string("9-999-99999-9"));   // Ok
item.combine(Sales("9-999-99999-9"));    // Ok
```

**Explicit keyword**

__Suppressing implicit conversions defined by constructors__: We can prevent the use of a constructor in a context that requires an implicit conversion by declaring the constructor as **explicit**. Now, neither constructor can be used to implicitly create a Sales object. The explicit keyword is meaningful only on constructors that can be called with a single argument. It’s only used on the constructor declaration inside the class, it’s not repeated on a definition made outside the class body.

```
explicit Sales(const std::string &s) : bookNo(s) { }
explicit Sales(std::istream&);
```

```
item.combine(null_book);    // Now is wrong
item.combine(cin);          // Now is wrong
```

__Explicit constructors can be used only for direct initialization__: One context in which implicit conversions happen is when we use the copy form of initialization (`=`). We cannot use an explicit constructor with this form of initialization; we must use direct initialization:

```
Sales item1(null_book);      // Direct initialization
Sales item2 = null_book;     // Error: Cannot use the copy form of initialization with an explicit constructor
```

When a constructor is declared `explicit`, it can be used only with the direct form of initialization. The compiler will not use this constructor in an automatic conversion.

__Explicitly using constructors for conversions__: Although the compiler will not use an explicit constructor for an implicit conversion, we can use such constructors explicitly to force a conversion:

```
item.combine(Sales(null_book));               // Argument explicitly constructed
item.combine(static_cast<Sales>(cin));   // static_cast can use an explicit constructor
```

In both cases, a temporary Sales object is constructed.

**Constructor initializer list**:

```
Sales(const std::string &s, usigned n, double p): book_num(s), revenue(p*n) { }
```

List of comma-separated member names, each of which is followed by that member’s initial value in parentheses (or curly braces).

When a member is omitted from the constructor initializer list, it is implicitly initialized using the same process as is used by the synthesized default constructor (in this case, the in-class initializers).

It’s usually best for a constructor to use an **in-class** initializer if one exists and gives the member the correct value. If your compiler doesn’t yet support in-class initializers, then every constructor should explicitly initialize every member of built-in type.

If we don’t explicitly initialize a member in the constructor initializer list (initializes data members), that member is default initialized (assigns values to the data members) before the constructor body starts executing.

Members that are const, references or class types that doesn’t define a default constructor must be initialized with a constructor initializer list.

Each member may be named only once in the constructor initializer. The order of initialization doesn’t matter, except when one member is initialized in terms of another.

```
class X {
    int i;
    int j;
public:
    X(int val): j(val), i(j) { }    // Error: i is initialized first, j second
};
```

A constructor that supplies default arguments for all its parameters also defines the default constructor.

**Defining a constructor outside the class body**:

```
Sales::Sales(std::istream &is) {
    read(is, *this);
}
```

Constructors have no return type. We must specify the class of which the constructor is a member.

Members that don’t appear in the constructor initializer list are initialized by the corresponding in-class iitializer (if there is one) or are default initialized.

**Delegating constructors**

A delegating constructor uses another constructor from its own class to perform its initialization. It delegates some or all of its work. In a delegating constructor, the member initializer list has a single entry that is the name of the class itself followed by a parenthesized list of arguments that must match another constructor in the class.

```
Sales_data() : Sales_data("", 0, 0) {}
Sales_data(std::string s) : Sales_data(s, 0, 0) {}
Sales_data(std::istream &is) : Sales_data() { read(is, *this); }
```

### Copy, assignment and destruction

Classes control how objects are **Initialized**, **Copied**, **Assigned**, **Destroyed**. If we don’t define these operations, the compiler will synthesize them for us. However, synthesized versions are unlikely to work correctly for classes that allocate resources that reside outside the class objects themselves. Classes that manage dynamic memory, generally cannot rely on the synthesized versions of these operations. Classes that need dynamic memory generally should use vectors and strings to manage the necessary storage because they avoid the complexities involved in allocating and deallocating memory and the synthesized versions of these classes work correctly.

### Defining a type member

```
typedef std::string::size_type pos;
```

```
using pos = std::string::size_type;
```

Members that define types must appear before they are used (so, they usually appear at the beginning of the class).

### Inline members

Small functions can benefit from being inlined. Member functions defined inside the class are automatically inline (implicitly). We can also explicitly declare a member function as **inline** as part of its declaration inside the class body or on the function definition outside the class body. It’s legal to specify inline on both the declaration and definition but doing so only on the definition outside the class makes it easier to read. Inline member functions should be defined in the same header as the corresponding class definition.

```
inline screen &screen::move(pos r, pos c) {
     pos row = r * width;
     cursor = row + c;
     return *this;
}
```

### Overloading member functions

Member functions may be overloaded as long as the functions differ by the number and/or types of parameters. The function-matching process is the same as for nonmember functions.

### static class members

Classes sometimed need members that are associated with the class, rather than with individual objects of the class type. Example: A bank account class might need a data member representing current prime interest rate. Here, we’d want to associate the rate with the class, not with each individual object. A member is associated with the class by adding the keyword `static` to its declaration (it can be `public` or `private`). The type of a static data member can be const, reference, array, class type and so forth. The static members of a class exist outside any object. Objects don’t contain data associated with static data members.

```
class Account {
public:
     void calculate() { amount += amount * interestRate; }
     static double rate() { return interestRate; }
     static void rate(double);
private:
     double amount;
     static double interestRate;
     static double initRate();
}
```

Similarly, `static` member functions are not bound to any object. They don’t have a this pointer, so they may not be declared as const, and we may not refer to this in the body of a static member. This restriction applies both to explicit uses of this and to implicit uses of this by calling a non-static member.

We can access a static member directly through the scope operator, without creating an object.

```
double r;
r = Account::rate();
```

We can use an object, reference or pointer of the class type to access a static member.

```
Account a1;
Account *a2 = &a1;
r = a1.rate();
r = a2->rate();
```

Member functions can use static members directly, without the scope operator. We can define static member function inside or outside of the class body. The keyword static only appears with the declaration inside the class body.

```
void Account::rate(double newRate) {
     interestRate = newRate;
}
```

As with any class member, when we refer to a class static member outside the class body, we must specify the class in which the member is defined. Because static data members are not part of individual objects of the class type, they are not defined when we create objects of the class, so they aren’t initialized by the class’ constructors. In general, we may not initialize a static member inside the class. Instead, we must define and initialize each static data member outside the class body. Like any other object, a static data member may be defined only once. Like global objects, static data members are defined outside any function. Once defined, they exist until the program completes.

We define a static data member similarly to how we define class member functions outside the class.

```
double Account::interestRate = initRate();
```
Once the class name is seen, the remainder of the definition is in the scope of the class, so we can use initRate without qualification as the initializer for rate. Even though initRate is private, we can use this function to initialize interestRate. The definition of interestRate, like any other member definition, has access to the private members of the class.

Ordinarily, class static members may not be initialized in the class body, but we can provide in-class initializers for static members that have const integral type and must do so for static members that are constexpr of literal type.

```
static constexpr int period = 30;
```

If the member is used only in contexts where the compiler can substitute the member’s value, then an initialized const or constexpr static need not be separately defined. However, if we use the member in a context in which the value cannot be substituted, there, must be a definition for that member. If an initializer is provided inside the class, the member’s definition must not specify an initial value:

```
constexpr int Account::period;    // Initializer provided in the class definition
```

Even if a const static data member is initialized in the class body, that member ordinarily should be defined outside the class definition.

A static data member can have incomplete type. In particular, it can have the same type as the class type of which it’s a member. A non-static data member is restricted to being declared as a pointer or a reference to an object of its class.

We can use a static member as a default argument. A non-static data member may not be used as a default argument because its value is part of the object of which it’s a member.


## Access control and encapsulation

### Access specifiers

We use **access specifiers** to enforce encapsulation:

- **public**: Members accessible to all parts of the program. Defines the interface.
- **private**: Members accessible to member functions. Encapsulates the implementation.

A class may contain zero or more access specifiers. Each access specifier specifies the access level of the succeeding members and remains in effect until the next access specifier or the end of the class body.

**Struct**: The only difference with a class is that the struct’s defaul access level is **public**, and the **class** one is **private**.

### Friends

A class can allow another function, class or member function of another class to access its non-public members by making that class or function a **friend** by including a declaration for that function preceded by the keyword friend.

```
class sales{
    friend sales add(const sales&, const sales&);
    friend std::istream &read(std::istream&, sales&);
    friend std::ostream &print(std::ostream&, const sales&);
public:
    // ...
}
```

Friend declarations may appear only inside a class definition, anywhere in the class. Friends are not members and are not affected by the access control of the section in which they are declared. It may be a good idea to group friend declarations together at the beginning or end of the class definition. A friend declaration only specifies access; we must also declare the function separately from the friend declaration (usually, in the same header as the class itself).

A friend function can be defined inside the class body. These functions are implicitly inline.

**Friendship between classes**

```
class Screen {
    friend class Window_mgr;
};
```

Member functions of a friend class can access all the members, including the non-public members. Frienship is not transitive (if `Window_mgr` has it own friends, they have no special access to Screen). Each class controls which classes or functions are its friends.

**Friend member function**

```
class Screen {
    friend void Window_mgr::clear(ScreenIndex);
};
```

**Overloaded functions and friendship**

Although overloaded functions share a common name, they are still different functions. A class must declare as a friend each function in a set of overladed functions that it wishes to make a friend.

**Friend declarations and scope**

Classes and non-member functions need not have been declared before they are used in a friend declaration. When a name first appears in a friend declaration, that name is implicitly assumed to be part of the surrounding scope. However, the friend itself is not actually declared in that scope. Even if we define the function inside the class, we must provide a declaration outside of the class itself to make that function visible.

```
struct X {
    friend void f() {
        // function body
    }
}
void f();
```


## Additional class features

### mutable data members

They are data members that we are able to modify, even inside a const member function. It’s never const, even when it’s a member of a const object. A const member function may change a mutable member. Any member function, including const functions, can change its value.

```
class Screen {
public:
    void some_member() const { ++access_ctr; }; 
private:
    mutable size_t access_ctr;
}
```

### Initializers for data members of class type

If we want a data member of class type default-initialized, the best way is an in-class initializer:

```
std::vector<Screen> screens{Screen(24, 80, ' ')};
```

When we initialize a member of class type, we are supplying arguments to a constructor of that member’s type. Here, we initialize our vector with a single element. In-class initializers must use either the = form of initialization or the curly braces {}.

### Class types

Every class defines a unique type. Two different classes define two different types even if they define the same members. We can refer to a class type directly:

```
Sales_data item1;              // default-initialized object 
class Sales_data item1;        // equivalent
```

We can declare a class without defining it:

```
class Screen;            // forward declaration
```

**Forward declaration**: Introduces the name of the class and indicates that it refers to a class type. After a declaration and before a definition is seen, this is an **incomplete type** (members aren’t known yet). We can use incomplete types in only limited ways:

- Define pointers or references to such types.
- Declare (but not define) functions that use an incomplete type as a parameter or return type.

A class must be defined before we can write code that creates objects of that type or before a reference or pointer is used to access a member of the type.

With one exception, data members can be specified to be of a class type only if the class has been defined. A class cannot have data members of its own type, but can have data member that are pointers or references to its own type:

```
class Link_screen {
    Screen window;
    Link_screen *next;
    Link_screen *prev;
};
```

### Aggregate classes

They give users direct access to its members and has special initialization syntax. A class is aggregate if:

- All of its data members are `public`
- Doesn’t define any constructors
- No in-class initializers
- No base classes or virtual functions

```
struct Data {
     int age;
     string name;
}
```

We can initialize the data members of an aggregate class by providing a braced list of member initializers, appearing in declaration order of the data members:

```
Data val = { 25, "Anna" };
```

If the list of initializers has fewer elements than the class has members, the trailing members are value initialized. It cannot contain more elements than the class has members. Drawback: If a member is added or removed, all initializations have to be updated.

### Literal classes

Classes whose data members are all of literal type. A non-aggregate class that meets the following restrictions is also a literal class:

- All data members must have literal type
- Must have at least one constexpr constructor
- If a data member has an in-class initializer, the initializer for a member of:

  - built-in type must be a constant expression.
  - class type  must use the member’s own constexpr constructor

- The class must use default definition for its destructor

These classes may have member functions that are constexpr (parameters and return type of a constexpr functions must be literal types). These member functions are implicitly const.

**constexpr constructors**

Although constructors cannot be const, constructors in a literal class can be constexpr functions. A constexpr constructor can be declared as = default (or as a deleted function). Otherwise, a constexpr constructor must meet the requirements of a constructor (cannot have return statement) and of a constexpr function (the only executable statement it can have is a return statement). As a result, the body of a constexpr constructor is typically empty. We define a constexpr constructor by preceding its declaration with the keyword constexpr.

A constexpr constructor must initialize every data member. The initializers must either use a constexpr constructor or be a constant expression. A constexpr constructor is used to generate objects that are constexpr and for parameters or return types in constexpr function.


## Class scope

Outside the class scope, ordinary data and function members may be accessed only through an object, a reference or a pointer using a member access operator. We access type members from the class using the scope operator. The name that follows the operator must be a member of the associated class.

```
Screen::pos ht = 25, wd = 100;
Screen scr(ht, wd, ' ');
char c = scr.get();
Screen *p = &scr;
c = p->get();
```

**Scope and members defined outside the class**

The class is a scope, so we must provide the class name and the function name when we define a member function outside its class. Outside of the class, the names of the members are hidden. Once the class name is seen, the definition is in the scope of the class, and now we can refer to other class members without qualification. The return type of a function normally appears before the function’s name.

```
class Window_mgr {
public:
    ScreenIndex addScreen(const Screen&);
};

Window_mgr::ScreenIndex Window_mgr::addScreen(const Screen &s) {
    screens.push_back(s);
    return screens.size() - 1;
}
```

To use ScreenIndex for the return type, we must specify the class in which that type is defined. The return type is seen before we’re in the scope of Window_mgr.

**Name lookup and class scope**

Name lookup (process of finding which declarations match the use of a name):

1. Look for a declaration of the name in the **block** in which it was used. Only names declared before are considered.
2. Look in the enclosing **scope/s**
3. If declaration isn’t found, **error**

Class definitions are processed in 2 phases:

1. Member declarations are compiled
2. Function bodies are compiled only after the entire class has been seen

Member function definitions are processed after the compiler processes all of the declarations in the class. Thus, member function bodies can use any name defined inside the class.

**Name lookup for class member declarations**

Names used in declarations, including names used for the return type (typedef) and types in the parameter list (string…), must be seen before they are used.

**Type names are special**: In a class, if a member uses a name from an outer scope and that name is a type, then the class may not subsequently redefine that name.

```
typedef double Money;
class Account {
    typedef double Money;           // Error
    // ...
};
```

Definitions of type names usually should appear at the beginning of a class.

**Normal block-scope name lookup inside member definitions**

1. Look for a declaration of the name inside the member function. Only declarations that precede the use of the name are considered
2. Look for a declaration inside the class
3. Look for a declaration in scope before the member function definition

**After class scope, look in the surrounding scope**: If the compiler doesn’t find the name in function or class scope, it looks for the name in the surrounding scope. If we want the name from the outer scope, we can ask for it explicitly using the scope operator.

```
void Screen::dumy_fcn(pos height) {
    cursor = width * ::height;         // which height? the global one
}
```

Even thought the outer object is hidden, it’s still possible to access that object by using the scope operator.

**Names are resolved where they appear within a file**. When a member is defined outside its class, the third step of name lookup includes names declared in the scope of the member definition as well as those that appear in the scope of the class definition.
