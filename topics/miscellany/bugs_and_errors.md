# Bugs and errors


## Table of Contents

+ [References](#references)
+ [Introduction](#introduction)
+ [Prevention](#prevention)
+ [Debugging](#debugging)
+ [Examples](#examples)

## References

- IEEE Computer Society (2025) _**Guide to the software engineering body of knowledge (SWEBOK) v4.0a**_. IEEE. Retrieved from [here](https://www.computer.org/education/bodies-of-knowledge#swebok).

## Introduction

**Software bug**: Design defect in computer software. It can range from minor to severe. A buggy software contains one or more bugs that affects it seriously. Bugs are caused by humans, they don't arise on their own. Some synonims of bug: error, mistake, fault, exception, glitch, defect.

**Mistake metamorphism**: A simple error in an early stage of the software development lifecycle can become a very serious error in the final stages. It's very important to fix errors as soon as possible; otherwise, they can be much harder and expensive to fix later.

**Software Development Process (SDP)**: Process of developing software. It usually divides a project into smaller tasks to ensure high-quality results. It may describe specific deliverables (artifacts to create and complete).

Compiled languages allow for detecting some typos (typographical errors) before runtime, which is earlier in the SDP than for an interpreted language. Some languages include features that make compilation fail if some errors are present, while interpreted languages will cause a failure later at runtime. Examples:

- Static type system (`float num = "5";` is syntactically correct, but fails type checking)
- Restricted namespaces
- Modular programming

Some languages exclude features that easily lead to bugs, at the expense of slower performance. Example: Java doesn't support pointer arithmetic, which are fast but may lead to segmentation faults or memory corruption if used incorrectly. 

Some languages include features that add runtime overhead in order to prevent common bugs. Example: runtime bounds checkings, and systems for recovering from out-of-bounds errors instead of crashing.

## Prevention

Different techniques can be used to prevent errors, such as:

- **Style guidelines**:

- **Defensive programming**: 

- **Specifications**: 

- **Testing**:

- **Agile practices**: 

- **Static analysis**: 

- **Instrumentation**: 

- **Open source**: 



## Debugging

**Programming errors** ("bugs"): Mistakes in software that cause incorrect behavior or failure. There're different types of bugs based on when and how they manifest, each requiring different methods for detection and resolution. The most common types are:

- **Syntax error**: The code violates the grammatical rules of the programming language, preventing compilation or interpretation (missing brackets, incorrect keywords, misplaced punctuation...). They're typically caught early by compilers/IDEs.
- **Runtime error**: Often caused by invalid operations (division by 0, accessing null pointer, trying to read a non-existing file...). They happen during program execution, usually leading to crashes or unexpected behavior.
- **Logical error**: Mistake in the program's algorithm or reasoning that results in incorrect output, even though the code runs without crashing (incorrect loop conditions causing infinite loops, flawed calculations...). It's often the most difficult to detect because no error message is generated.
- **Semantic error**: Related to the meaning or context of the code, such as using a programming construct or data type incorrectly, even if the syntax is valid. They can lead to unintended behavior that is hard to trace.

Other less common types of errors are:

- **Security error**: Vulnerabilities that can be exploited by attackers to compromise data integrity, confidentiality, or system availability. Examples: Buffer overflows, SQL injection, cross-site scripting (XSS).
- **Memory leaks**: Type of resource error where allocated memory is not properly released, leading to gradual performance degradation or system crashes over time.
- **Boundary condition error**: It occurs when the program fails to handle input values at the extreme ends of acceptable ranges, such as maximum or minimum values.
- **Concurrency error**: Found in multi-threaded or distributed systems. Error that arises when multiple processes access shared resources simultaneously. Examples: race conditions, deadlocks, and other synchronization issues.
- **Linker errors**: These occur during the linking phase of compilation, typically due to missing or conflicting libraries or undefined symbols.
- **Performance errors**: These affect the speed, stability, or resource consumption of the software, often leading to slow response times or high memory usage.
- **Type error**: Like passing an argument of the wrong type to a function.
- **Declaration error**: Like not declaring a name, misspelling it or forgetting `std::`.

These errors can be prevented or mitigated through practices such as code reviews, unit testing, using debuggers, validating inputs, and employing static code analysis tools.

It’s good practice to correct errors in the sequence they are reported. If not, a compiler may report more errors than actually are present (cascading effect). Recompile the code after each fix (cycle edit-compile-debug).

**Debugging methods**:

- **Look for location**: Use prints/breakpoints to find where the program stops working.
- **Look by omission**: Don’t execute parts of your program until the bug happens. This will show which part of the program causes the bug.
- **Check new additions**: Before implementing X, there were no problems. After X, there are problems. Thus, analyze X.
- **Compiler optimizations**: While testing for finding a bug origin, a certain `if(condition)` crashed the application when it had some content in his body, but didn’t when it hadn’t. Reason? Compiler optimized code by deleting empty conditional blocks that will never execute.
- **Non-sensical bugs**: Some bugs make no sense (they happen at random points in execution with an unpredictable behavior, with no clear patterns). Probably, you overwrote some part of memory belonging to other variables, which may have consequences at some point. Look out for dynamic memory allocations and de-allocations. Example cases: Using garbage memory as if there was an allocated object, or using memory belonging to an existing object as if it belonged to another
- **Macros**: Use macros to activate/deactivate debugging messages in certain parts or topics. Alternatively, use logs.

Absurd error messages could be solved by removing new code recently added until things work properly.


Errors that cause a crash can be located easier than those than don't crash. One techniques for those that don't crash is to omit code.



## Examples

Sometimes program doesn't stop working at some point (semantic error?)

Multithreading

Overflow

defective update

- **GPU with little memory**

When using my graphics engine in a different computer, it didn’t work. A window appeared saying that I used too much memory from the GPU. It was weird because I was not using that much memory. I deduced that maybe the integrated GPU was being used instead of the dedicated GPU. Then, I modified the conditions my application was applying (through Vulkan) to select one of the available GPUs. After this, the correct GPU was used and everything worked fine.

- **Tree construction**

During the render loop, I required a tree data structure to be updated. I was building a tree and using it. After this, I was building a new one and, when it was complete, the old one was replaced with the new one, and so on. However, after a few trees were created and replaced, the program was crashing (invalid memory access or stack overflow). Before replacing one tree with the next, the new tree was being traversed for a final check, and that’s where the crash happened.

This made me think that the tree being passed was badly built (most crashes happened while accessing the Node::isLeaf() method). After a check, I confirmed that the correct number of nodes and leaves were being built, so it looked that the tree construction was right. Surely I was missing something at tree construction, but I couldn’t see what. However, it was late and I was sleepy, so I left the problem for the next day.

The next day, after waking up, I stayed in bed with my eyes closed, thinking about the tree problem (probably, the best time of the day to think). Shortly after, I remembered that after replacing one tree with the other, I was deleting all the nodes of the old tree, and then building the new tree from the root node pointer. This root pointer was pointing to a no longer valid address, which could have garbage. The fact that I was not setting it to nullptr caused that the tree-construction system thought that the tree was already built, so it didn’t built it. Then, when traversing the tree, it was traversing just garbage.

Do you remember that I said that I confirmed that the correct number of nodes were being built? I was seeing the results of the previous tree (first tree), which was being built correctly since the root was nullptr at the beginning. However, I had assumed that the new tree was being built, and I thought those result were from a new tree.

- **Transformation matrices**

When rendering, sometimes what I want to render doesn’t appear on screen, and no exception or error pops up. When this happens, I tend to look at the UBOs update process since passing wrong values for the transformation matrices show no errors, but these garbage values are often very high (or very low), which makes the object to render in very far away positions, not visible from where the camera is (in fact, invisible, since they are beyond the far clipping plane). This mistake is very easy to make.

- **The rendering gap**

I was using Vulkan for rendering some objects. At some point, I wanted object A to disappear and be replaced with object B. However, what actually happened was that, after object A disappeared, object B was not rendered in his place, but it was in the next frame (i.e., object B was missing during one frame). I elaborated a few theories about why this could be happening:

- Object B construction was wrong: After some checks, the construction was ok and it made no sense that the bug were originated here. It was correctly loaded into GPU. The command buffer was update properly. The UBOs were updated.
- Some Vulkan synchronization issue: Maybe, while creating object B, there was some operation that happenned asynchronously and it was not ready yet when I tried to render B. I studied Vulkan synchronization in order to find the problem, but I found no problem.
- Some problem with UBOs update: The fact that the object was missing makes think that it was using garbage values for the UBO. However, correct values were stored in the UBO.

All of these possible bug sources were checked and no problem was found. However, I strongly felt that the source was most likely caused somehow by an UBO update issue (it had happened before and was an easy source of problems).

I made a couple of simplified functions that tried to replicate the bug. One of them didn’t replicate the bug. Interestingly, such function was the only one rendering an object that didn’t required UBOs (no transformation matrices were required because it was being rendered directly in Normalized Device Coordinates).

I faced this error for about 2 weeks without success. I ended up burned out from this bug and then I abandoned it for about 2 weeks. One morning I decided to give it a try. To my surprise, I found the source of the bug in half an hour, and fixed it in 15 minutes

The problem was that, though I was updating the UBO (CPU), I was not passing that data to the GPU during the first frame. This happened because I only passed the UBO data from the objects that were stored in a container containing those objects already being rendered. However, my object was not there yet, but it was stored there a few lines below. I had overlooked that fact.

Originally, I followed these steps each frame: construct object and update UBO (1), pass UBO to GPU (2), move object to container (3), update CB (4). To fix the problem, I simply swapped step 2 with step 3.

- **Parallel simple task**

One thread got stuck while the other was running. The running thread contained a tight loop with a simple task (example: a loop that did a very simple and fast task), so it looked like no time for rest was given to that thread (**Thread starvation**, or **CPU hogging**). This meant that there was no opportunity for the OS to change execution from this thread to the other, so execution remained in one thread.

- **Non-destructible object**

One thread got stuck while the other kept running. This happened because thread A was trying to delete an object that was in use in thread B. In other words, the object had to be destroyed in thread A, so its destructor was called. However, such object was being used in thread B, so the execution of the destructor in thread A was not possible and the execution there was halted.

- **Application works half of the times**

After executing the application, the bug made the program to stop working half of the times while the other half times it worked perfectly. It was due to the fact that the application was using some garbage value stored in a deleted memory address. Such value was sometimes correct (example: it was zero) and sometimes incorrect (example: it was non-zero).

- **Map key doesn’t work**

The application output an exception. It contained an object of type `std::map<glm::vec3, element>`. A `std::map` is usually implemented as a red-black tree (self-balancing binary search tree). Keys are sorted by using the comparison function `Compare`. However, `glm::vec3` doesn’t have a `Compare` method, so it cannot be used as key. I solved this by using a `std::tuple<float, float, float>` as a key.

- **Not a number**

The application was crashing. After some investigation, I discovered that one variable was sometimes saving `nan(ind)` (_Not A Number_) values. This variable looked like float var = acos(param). It turns out that when we compute acos on param > 1 or param < -1, the result is nan. I solved this by clamping param in the range [-1, 1].

- **Variables with similar name**

I was getting wrong results in my application. It took a long time to realize that I was updating a function’s local variable instead of the correct class member. Both had similar names (gDir and gVec) and, because I didn’t pay enough attention, I overlooked the fact that I was updating gDir (which was correct) but I wasn’t updating also gVec (member) because I considered that it was already updated.

- **Copy constructor missing**

After implementing a new system for loading data for rendering, somehow data was not being rendered. I couldn’t find easily where the problem was. I noted that, at the end of the execution, the program was breaking when trying to delete objects previously allocated dynamically. This suggested me that some part of memory was being used incorrectly (maybe using garbage memory as if there was an allocated object, or using memory belonging to an existing object as if it belonged to another). This made me look in the new code for objects that required dynamic allocation. Finally, I found that there was a class that required a copy constructor to avoid copying directly a pointer to a dynamically allocated object (instead of allocating a new identical object and getting its pointer). My theory:

An object of type A was created and then deleted, but a pointer to this garbage memory was still in use.
New objects are allocated in this garbage memory.
Garbage memory is used incorrectly by the buggy pointer.
The program crashes when trying to delete the new objects. Alternatively, they’re deleted successfully, but program crashes when trying to delete the buggy pointer.

- **Non-sensical error**

There are errors that make absolutely no sense. They can even change from one compilation to another (even when code hasn’t changed at all). Probably the issue is that you wrote on memory reserved for other resources instead of the intended resource (example: your could edit all the element in an array and continue editing memory beyond the array limit by mistake). The resulting error is unpredictable and depends on what was on the memory before it was overwritten by mistake.

- **Missing token**

A compiler error (Unexpected token/s preceding ';') points to the declaration of a member variable (SomeType* obj) in the file A.hpp. The class SomeType is defined in another file which is already included (#include "B.hpp") in file A.hpp. Everything looks fine.

Problem: B.hpp contains a #include "C.hpp", and file C.hpp contains a #include "A.hpp", which is a circular reference to file A.hpp. (A > C > B > A…). This makes compiler don’t understand well SomeType* obj.

Solution: Put a forward declaration class SomeType; (instead of #include "B.hpp") in file A.hpp, and put an include (#include "B.hpp") on file B.cpp (if members of B of SomeType are used there).

- **Bad construction**

A member of a class appears to be not correctly initialized. However, checking the constructor, everything looks fine. 

Problem 1: The issue was not there, but in the copy-constructor/move-constructor/copy-assignment operator.

Problem 2: The member uses other members of the class to initialize itself. However, those members aren't yet initialized. Remember, members are initialized in the same order as they appear in the class definition.

- **Wrong syntax errors**

A syntax error message persists even though the code is correct and such error should not appear. Example: `enum MyEnum {A, B, C}` appears before `MyClass::MyClass(MyEnum value);`, but the IDE says that `identifier "MyEnum" is undefined` at the method declaration or definition.

This might be the result of another syntax error that is not detected by the IDE and that has nothing to do with the printed error. The printed error may disappear after fixing the real error, which can be difficult to detect since the IDE is not helping at all. Probable real errors are:

- In a constructor method, an argument is assigned to a member variable but they have different type.
- Missing includes and/or forward declarations.
