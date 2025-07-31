# Debugging

## Table of Contents
+ [Errors](#errors)
+ [Aids for debugging](#aids-for-debugging)
+ [Exception handling](#exception-handling)
+ [macros in MVS to avoid warnings](#macros-in-mvs-to-avoid-warnings)


## Errors

Most common kind of errors a compiler will detect:

- **Syntax errors**: Grammatical error
- **Type errors**: Like passing an argument of the wrong type to a function
- **Declaration errors**: Like not declaring a name, misspelling it or forgetting std::

It’s good practice to correct errors in the sequence they are reported. If not, a compiler may report more errors than actually are present (cascading effect). Recompile the code after each fix (cycle edit-compile-debug).


## Aids for debugging

The program may contain debugging code that is executed only while the program is being developed. When it’s completed, the debugging code is turned off. Use 2 preprocessor facilities:

- `assert`
- `NDEBUG`

### assert preprocessor macro

**Preprocessor macro**: Preprocessor variable that acts somewhat like an inline function.

`assert` macro takes a single expression and uses it as a condition. If the expression is false, assert writes a message and terminates the program. If it’s true, it does nothing. Defined in `<cassert>`. Used to check for conditions that “cannot happen”. It’s good idea to avoid using the name assert for our own purposes.

Preprocessor names are managed by the preprocessor, not the compiler, so we can use preprocessor names directly and don’t provide a using declaration for them. As with preprocessor variables, macro names must be unique within the program.

```
assert(expr);
```

```
assert(word.size() > threshold);
```

### NDEBUG preprocessor variable

If it is defined, assert does nothing. By default, NDEBUG is not defined (so, by default, assert performs a run-time check). Two ways to “turn off” debugging:

- Providing:

```
#define NDEBUG
```

- Defining it with the command-line (if the compiler provides this option) (same effect as writing `#define NDEBUG` at the beginning of `main.C`):

```
$ CC -D NDEBUG main.C      # use /D with the Microsoft compiler
```

In addition to using assert, we can write our own conditional debugging code using NDEBUG. If NDEBUG is not defined, the code between the #ifndef and the `#endif` is executed. If NDEBUG is defined, that code is ignored:

```
void print(const int ia[], size_t size) {
    #ifndef NDEBUG
    cerr << _ _func_ _ << ": array size is " << size << endl;
#endif
}
```

**Predefined names**:

- `__func__`: This is defined in every function. It is a local static array of const char that holds the name of the function (example: main).

Preprocessor defines 4 other names:

- `__FILE__`: String literal containing the name of the file (wdebug.cc).
- `__LINE__`: Integer literal containing the current line number (27).
- `__TIME__`: String literal containing the time the file was compiled (20:50:03).
- `__DATE__`: String literal containing the date the file was compiled (Jul 10 2012).

**Others**:

- `typeid(*this).name()`: Name of the class (call it from a method)


## Exception handling

See chapter [Exception handling](https://github.com/AnselmoGPP/Learn_Computer_Science/blob/master/topics/cpp/exception_handling.md).


## macros in MVS to avoid warnings

**Error example**:

```
C4996    ‘strcpy’: This function or variable may be unsafe. Consider using strcpy_s instead. To disable deprecation, use _CRT_SECURE_NO_WARNINGS. See online help for details.
```

**Solution in Visual Studio**: Configuration properties > C/C++ > Preprocessor > Preprocessor definitions > Insert `_CRT_SECURE_NO_WARNINGS`
