# Exception handling

Exceptions are **run-time anomalies** that exists outside the normal functioning of a program. They are generally used when one part of a program detects a problem that it cannot resolve and the program cannot continue (invalid input, lost database…). The detecting part signals the problem without knowing what part of the program will deal with the exceptional condition. Having signaled what happened, the detecting part stops processing. Exception handling involves:

- **throw expressions**: Used by the detecting part to indicate that it encountered something it cannot handle (a throw **raises** an exception).
- **try blocks**: Used by the handling parts to deal with an exception. Starts with try and ends with one or more __catch clauses__.
- **catch clauses / exception handlers**: Exceptions thrown from code that is executed inside a try block are usually handled by one of the catch clauses.
- **exception classes**: Pass information about what happened between a throw and an associated catch.

## throw expression

The detecting part of a program uses a throw followed by an expression to raise an exception. A throw expression is usually followed by a semicolon. Throwing an exception terminates the current function and transfers control to a handler.

**Standard library exception types** (`<stdexcept>`): We can throw an expression that is an object of one of these types (`runtime_error`…).

```
if(book1.number() != book2.number())
throw runtime_error("Data must refer to same ISBN");
cout << book1 + book2 << end; // If we reach this line, the books have same number
```

## try block

Following the try block is a list of one or more catch clauses. Code inside the try block throws a runtime_error.

```
try {
    program-statements
} catch (exception-declaration) {
    handler-statements
} catch (exception-declaration) {
    handler-statements
} …
```

When a catch is selected to handle an exception, the associated block is executed. Once the catch finishes, execution continues with the statement immediately following the last catch clause of the try block.

Program-statements inside the try constitute the normal logic of the program. Variables declared inside a try block are inaccessible outside the block (even for the catch clauses).

```
try { throw 20; }
catch (int e) { cout << "Exception " << e; }
```

```
try { throw 20; }    // Non controlled exception (no catch to handle it)
catch(string a) { cout << "Exception"; }
```

```
double a, b;
while(cin >> a >> b) {
    try {
        if(b==0) throw "Data must be non-zero";
        cout << a/b;
    }
catch(string a) {
    cout << a << "Try again? (y/n) ";
    char c;
    cin >> c;
    if (!cin || c=='n') break;
    }
}
```

```
double a, b;
while(cin >> a >> b) {
    try{
        if(b==0) throw runtime_error("b must not be zero");
        if(a > b) throw string("a must be bigger than b");
        cout << a/b;
    }
catch(runtime_error err) {
    cout << err.what() << "Try again? (y/n) ";
    char c;
    cin >> c;
    if(!cin || c=='n') break;
}
catch(string str) {
    cout << str;
    break;
    }
}
```

**err** has type `runtime_error`. You must initialize `runtime_error` by giving a string or C-style character string (which provides additional information about the problem). **`what()`** is a member function of the `runtime_error` class. Each of the `runtime_error` classes defines a member function named `what()` that takes no arguments and return a C-style character string (`const char*`), which is a copy of the string used to initialize the object.

In **complicated systems**, the execution path of a program may pass throug multiple try blocks before encountering code that throws an exception. Example: A try block might call a function that contains a try, which calls another function with its own try, and so on. The search for a handler reverses the call chain. The function that threw the exception is searched first. If no matching catch is found, that function terminates. The function that called the one that threw is searched next, and so on, until a catch of an appropriate type is found. If no appropriate catch is found, execution is transferred to a library function named **terminate** (its behaviour is system dependent but is guaranteed to stop further execution of the program.

Exceptions that occur in programs that don’t define any try blocks are handled by calling **terminate** and exiting the program.

Writing **exception safe code** is hard. Exception interrupt the normal flow of a program. When this occurs, some computations that the caller requested may have been done, while others remain undone. Programs that properly “clean up” during exception handling are __exception safe__. Some programs use exceptions simply to terminate the program, they don’t generally worry about exception safety.

## Standard exceptions

C++ library defines several classes that it uses to report problems encountered in functions in the standard library, but they are also intended to be used in the programs that we write. They are defined in 4 headers:

- `<exception>`

  - **exception**: Comunicates only that an exception occurred.

- `<stdexcept>`

  - `runtime_error`: Problem that can only be detected at run time
  - `range_error`: Result generated outside the range of meaningful values
  - `overflow_error`: Overflowed computation
  - `underflow_error`: Underflowed computation
  - `logic_error`: Error in the logic of the program
  - `domain_error: Argument for which no result exists
  - `invalid_argument: Inappropriate argument
  - `length_error: Attempt to create an object larger than its maximum type size
  - `out_of_range: Used a value outside the valid range

- `<new>`

  - `bad_alloc`

- `<type_info>`

  - `bad_cast`

The library exception classes have only a few operations. We can **create**, **copy** and **assign** objects of any of the exception types.

**Initialization**: We can only default initialize exception, bad_alloc and bad_cast objects; you cannot provide an initializer. The other types can be initialized from either a string or a C-style string, but we cannot default initialize them; we must supply an initializer (used to supply additional information about the error).

The exception types define only a single operation named `what()`. It takes no arguments and returns a const char* that points to a C-style character string (to provide some description of the exception thrown). For the types that take a string initializer, what() returns that string; for the other types, returns varies by compiler.