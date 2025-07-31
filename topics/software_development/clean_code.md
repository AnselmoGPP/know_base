# Clean code

<br>![flow image](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/resources/flow.jpg)


## Table of Contents

+ [References](#references)
+ [Clean code](#clean-code)
+ [Meaningful names](#meaningful-names)
+ [Functions](#functions)
+ [Comments](#comments)
+ [Formatting](#formatting)
+ [Objects and Data structures](#objects-and-data-structures)
+ [Error handling](#error-handling)
+ [Unit tests](#unit-tests)
+ [Classes](#classes)
+ [Systems](#systems)
+ [Emergence](#emergence)
+ [Concurrency](#concurrency)
+ [Successive refinement](#successive-refinement)
+ [JUnit internals](#junit-internals)
+ [Refactoring](#refactoring)
+ [Smells and Heuristics](#smells-and-heuristics)


## References

- Robert C. Martin (2009) _**Clean code**_. Pearson Education, Inc. Boston.


## Clean code

To make good code we have to learn **craftmanship** through study (principles, patterns, practices, and heuristics) and practice (work).

Code represents the details of the **requirements**. At some level those details cannot be ignored or abstracted; they have to be specified. Specifying requirements in such detail that a machine can execute them IS programming. Such a specification IS code. Code is really the language in which we ultimately express the requirements. There will always be code because we will never eliminate necessary precision.

**Bad code can slow you down**. Teams that moved fast at the beginning may be significantly slowed down after some time due to bad code. Every change makes the code messier and decreases the team's productivity, until the code cannot be cleaned up and productivity is zero. Keeping code clean is not just cost effective, it's a matter of professional survival. The code has to be kept as clean as possible at all times. Writing clean code requires the disciplined use of many little techniques.

**Clean code** definitions: 

- Elegant and efficient code. Straightforward logic (making bugs hard to hide), minimal dependencies (to ease maintenance), complete error handling, good performance (so it doesn't tempt to make it messier). Clean code does one thing well (bad code tries to do too much). Bad code tempts the mess to grow (changes on bad code tend to make it worse).
- Simple and direct. Readable. The designer's intent is clear.
- It can be read and enhanced by another developer. It has unit and acceptance tests. Meaningful names. It provides only one way of doing one thing. Clear and minimal API.
- It cannot be made better. Done by someone who cares.
- Simple code runs all tests, contains no duplication, expresses all design ideas in the system, and minimizes the number of entities (classes, functions...). Tiny abstractions.

What is described on this book is our school of thought of clean code. We claim we are right, but not in an absolute term. We don't necessarily invalidate other schools. We recommend to learn from them as well.

When we try to write code we constantly have to read old code. We spend much more time reading code than writing it. We want code that is easy to read code, which in fact makes it easy to write too.

Code has to be kept clean over time. To do so, leave the code cleaner than you found it (continuous improvement). Check-in the code a little cleaner than when you checked it out. Otherwise, code rots and degrades as time passes.


## Meaningful names

Names are everywhere (variables, functions, arguments, classes, packages, source files, directories, jar files...). Some rules for creating good names are:

- **Use intention-revealing names**: It should tell why it exists, what it does, and how it's used. If the name requires a comment, it doesn't reveal its intent. Choosing good names takes time but saves more than it takes. Take care with your names and change them when you find better ones. The context should be explicit in the code (the problem is not the code's simplicity, but its implicity).

- **Avoid disinformation**: Avoid leaving false clues that obscure the meaning of code. Spelling similar concepts similarly is information, but inconsistent spellings is disinformation. Examples:
  - Names with meaning that vary from our intended meaning (`hp` instead of `hypotenuse`).
  - Don't name a group of accounts `accountList` if it's not a `List` container. Instead, you can use `accounts`, `accountGroup`, etc.
  - Beware of using names which vary in small ways (like `XYZControllerForEfficientHandlingOfStrings` and `XYZControllerForEfficientStorageOfStrings`)

- **Make meaningful distinctions**: Writing code solely to satisfy a compiler creates problems for programmers. Avoid noninformative names. Distinguish names so the reader knows what the differences offer. Examples to avoid:
  - Identical names: Since we cannot use the same name to refer to two different things in a scope, we might be tempted to change one name arbitrarily (misspelling, add numbers, add noise words...) (like `klass` because `class` is reserved, or ). If names must be different, they should also mean something different.
  - Noninformative names: Instead of `copyChars(char* a1, char* a2)` write `copyChars(char* source, char* destination)`.
  - Noise words (redundant words):
    - `ProductInfo` and `ProductData` are different words but mean the same (similar to `zork` and `theZork`).
    - `variable` should never appear in a variable name, nor should `table` appear in a table name. Use `name` instead of `nameString`.

- **Use pronounceable names**: This way, you can discuss them without sounding like an idiot.

- **Use searchable names**: Single-letter names and numeric constants are not easy to locate. Single-letter names could be used ONLY as local variables inside short methods (the length of a name should correspond to the size of its scope).

- **Avoid encodings**:
  - Encoding type or scope information into names adds an extra burden of deciphering. They are difficult to pronounce, easy to mis-type, and require to know another encoding "language".
  - There's no need to prefix member variables with `m_` anymore (classes and function should be small enough that you don't need them, and IDEs nowadays highlight them). 
  - If I have one class with the implementation and another with the interface, it's preferable to encode the implementation (`ShapeFactoryImp`) than the interface (`ShapeFactory`). The user doesn't need to know that they're using an interface.

- **Avoid mental mapping**: Readers shouldn't have to mentally translate your names into other names they already know. Write for clarity.
  - A loop counter can be named `i`, `j`, or `k` because its scope is very small and they're traditional names for loop counters.

- **Class names**: Classes and objects should have noun or noun phrase names (`Customer`, `WikiPage`, `Account`, `AddressParser`). They should not be a verb. Also, avoid words like `Manager`, `Processor`, `Data`, or `Info` in the name.

- **Method names**:
  - They should have verb or verb phrase names (`postPayment`, `deletePage`, `save`).
  - Accessors, mutators, and predicates should have a prefix (`get`, `set`, `is`) and their value (`getName`, `setName`, `isReady`).
  - When constructors are overloaded, use static factory methods (they return an instance of a class) with names that describe the arguments (`Complex point = Complex.FromRealNumber(23.0)` instead of `Complex point = Complex(23.0)`). Enforce their use by making the corresponding constructors private.

- **Don't be cute**: Choose clarity over entertainment value (`DeleteItems` instead of `HolyHandGrenade`). Avoid colloquialisms, slang, and jokes. Say what you mean. Mean what you say.

- **Pick one word per concept**: Pick one word for one abstract concept and stick with it. It's confusing to have `fetch`, `retrieve`, and `get` as equivalent methods of different classes.








57/378


## Functions
## Comments
## Formatting
## Objects and Data structures
## Error handling
## Unit tests
## Classes
## Systems
## Emergence
## Concurrency
## Successive refinement
## JUnit internals
## Refactoring
## Smells and Heuristics

