# Design patterns

## Table of Contents
+ [References](#references)
+ [Introduction](#introduction)
+ [Case study: Designing a document editor](#case-study:-designing-a-document-editor)


## References
- Erich Gamma, Richard Helm, Ralph Johnson, John Vlissides (1994) _**Design patterns. Elements of object-oriented software**_. Addison-Wesley. Retrieved from [link1](http://www.uml.org.cn/c++/pdf/designpatterns.pdf), [link2](http://www.grch.com.ar/docs/unlu.poo/Gamma-DesignPatternsIntro.pdf), [link3](https://github.com/TushaarGVS/Design-Patterns-Mentorship/blob/master/Erich%20Gamma%2C%20Richard%20Helm%2C%20Ralph%20Johnson%2C%20John%20M.%20Vlissides-Design%20Patterns_%20Elements%20of%20Reusable%20Object-Oriented%20Software%20%20-Addison-Wesley%20Professional%20(1994).pdf).
- [Sourcemaking](https://sourcemaking.com/design_patterns)
- [MVC design pattern](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller)


## Introduction

Designing reusable object-oriented software is hard. You have to:

- Find pertinent objects
- Factor them into classes at the right granularity
- Define class interfaces
- Define inheritance hierarchies
- Establish key relationships among them

The design should be specific to the problem at hand but also general enough to address future problems and requirements. Furthermore, you want to avoid redesign, or at least minimize it. A flexible and reusable design is difficult to get.

Experienced designers discovered that certain patterns of classes and communicating objects were very useful for solving specific design problems and make object-oriented designs more flexible, elegant and reusable. They can apply these patterns immediately to solve design problems without having to rediscover them.

### Types

A **pattern** describes a problem that happens very often in our environment, and then describes the core of the solution to it in such a way that you can use this solution a million times over without ever doing it the same way twice. A pattern has 4 elements:

- **Name**: Describes a design problem, its solutions, and consequences in one/two words.
- **Problem**: Describes when to apply a pattern.
- **Solution**: Elements that make up the design, their relationships, responsabilities and collaborations.
- **Consequences**: Results and trade-offs of applying the pattern.

**Design patterns**: Descriptions of communicating objects and classes that are customized to solve a general design problem in a particular context.

<br>![design patterns table](https://raw.githubusercontent.com/AnselmoGPP/Learn_Computer_Science/master/topics/software_development/resources/design_patterns_table.png)

**Purpose**: What a pattern does.

- **Creational**: Relative to object creation.
- **Structural**: Deals with the composition of classes or objects.
- **Behavioral**: Characterizes the ways in which classes or objects interact and distribute responsibility.

**Scope**: Specifies whether the pattern applies primarily to classes or objects

- **Class**: Deals with relationships between classes and their sub-classes (inheritance). They are static-fixed at compile-time.
- **Object**: Deals with object relationships, which can be changed at run-time.

**Creational**…

- **class patterns** defer some part of object creation to subclasses.
- **object patterns** defer it to another object.

**Structural**…

- **class patterns** use inheritance to compose classes.
- **object patterns** describe ways to assemble objects.

**Behavioral**…

- **class patterns** use inheritance to describe algorithms and flow of control.
- **object patterns** describe how a group of objects cooperate to perform a task that no single object can carry out alone.

**Creational patterns**:

- **Class**:
  - **Factory method**: Define an interface for creating an object, but let subclasses decide which class to instantiate. It lets a class defer instantiation to subclasses.
- **Object**:
  - **Abstract factory**: Provide an interface for creating families of related or dependent objects without specifying their concrete classes.
  - **Builder**: Separate the construction of a complex object from its representation so
 that the same construction process can create different representations.
  - **Prototype**: Specify the kinds of objects to create using a prototypical instance, and create new objects by copying this prototype.
  - **Singleton**: Ensure a class only has one instance, and provide a global point of access to it.

**Structural**:

- **Class**:
  - **Adapter class**: Convert the interface of a class into another interface clients expect. It let classes work together by making their interfaces compatible.
- **Object**:
  - **Adapter object**: Convert the interface of an object into another interface clients expect. It let objects work together by making their interfaces compatible.
  - **Bridge**: Decouple an abstraction from its implementation so that the two can vary
 independently.
  - **Composite**: Compose objects into tree structures to represent part-whole hierarchies. It lets clients treat individual objects and compositions of objects uniformly.
  - **Decorator**: Attach additional responsibilities to an object dynamically. It provides a flexible alternative to subclassing for extending functionality.
  - **Facade**: Provide a unified interface to a set of interfaces in a subsystem. It defines a higher-level interface that makes the subsystem easier to use.
  - **Flyweight**: Use sharing to support large numbers of fine-grained objects efficiently.
  - **Proxy**: Provide a surrogate or placeholder for another object to control access to it.

**Behavioral**:

- **Class**:
  - **Interpreter**: Given a language, define a represention for its grammar along with an interpreter that uses the representation to interpret sentences in the language.
  - **Template method**: Define the skeleton of an algorithm in an operation, deferring some steps to subclasses. Template Method lets subclasses redefine certain steps of an algorithm without changing the algorithm's structure.
- **Object**:
  - **Chain of responsability**: Avoid coupling the sender of a request to its receiver by giving more than one object a chance to handle the request. Chain the receiving objects and pass the request along the chain until an object handles it.
  - **Command**: Encapsulate a request as an object, thereby letting you parameterize clients with different requests, queue or log requests, and support undoable operations.
  - **Iterator**: Provide a way to access the elements of an aggregate object sequentially without exposing its underlying representation.
  - **Mediator**: Define an object that encapsulates how a set of objects interact. Mediator promotes loose coupling by keeping objects from referring to each other explicitly, and it lets you vary their interaction independently.
  - **Memento**: Without violating encapsulation, capture and externalize an object's internal state so that the object can be restored to this state later.
  - **Observer**: Define a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.
  - **State**: Allow an object to alter its behavior when its internal state changes. The object will appear to change its class.
  - **Strategy**: Define a family of algorithms, encapsulate each one, and make them interchangeable. Strategy lets the algorithm vary independently from clients that use it.
  - **Visitor**: Represent an operation to be performed on the elements of an object structure. Visitor lets you define a new operation without changing the classes of the elements on which it operates.

The simplest and most common patterns are: Abstract factory, Adapter, Composite, Decorator, Factory method, Observer, Strategy, Template method.

### Relationships

Some patterns are often used **together** (e.g.: Composite + Iterator/Visitor). Some are **alternatives** (Prototype, Abstract factory). Some result in **similar designs** (Composite, Decorator).

<br>![relationships](https://raw.githubusercontent.com/AnselmoGPP/Learn_Computer_Science/master/topics/software_development/resources/relationships.png)

### Solving design problems

- **Finding appropriate objects**

Design patterns help you identify less-obvious abstractions and the objects that can capture them.

- **Determining object granularity**

Objects can vary tremendously in size and number (from everything down to the hardware, to all the way up to entire applications).

- **Specifying object interfaces**

Objects are only known through their interfaces, and interfaces say nothing about the object’s implementation. The interface is the set of operations allowed by the object, wich are defined by their **signatures** (operation’s name, parameters and return values). A **type** is a name used to denote a particular interface. A type can be a sub-type: a sub-type has an interface that contains the interface of its super-type (sub-type **inherits** from its super-type).

**Dynamic binding**: It’s the run-time association of a request to an object and one of its operations. So, issuing a request doesn’t commit you to a particular implementation until run-time. Then, you can write programs that expect an object with a particular interface, knowing that any object that has the correct interface will accept the request. Moreover, dynamic binding lets you substitute objects that have identical interfaces for each other at run-time (**polymorphism**).

**Polymorphism**: It lets a client object make few assumptions about other objects beyond supporting a particular interface. It simplifies the definitions of clients, decouples objects from each other and lets them vary their relationships to each other at run-time.

Design patterns help you define interfaces by identifying their key elements and the kinds of data that get sent across an interface. They might also tell you what not to put in the interface (Memento). They also specify relationships between interfaces (Decorator, Proxy, Visitor).

- **Specifying object implementations**

An object implementation is defined by its class. The class defines the object’s internal _data_ and representation, and defines the _operations_ the object can perform. Objects are created by instantiating a class (the object is an instance of the class), and then some storage is allocated for the object’s internal data (instance variables) and associates the operations with these data.

**Class inheritance**: New classes can be defined in terms of existing classes. When a sub-class inherits from a parent class, it includes the definitions of all the data and operations that the parent class defines. Objects that are instances of the subclass will contain all data defined by the subclass and its parent classes, and they’ll be able to perform all operations defined by both.

**Classes**:

- **Abstract class**: It defines a common interface for its sub-classes. I defers some or all of its implementation to operations defined in sub-classes, hence it cannot be instantiated. The operations that it declares but doesn’t implement are **abstract operations**.
- **Concrete class**: A class that is not an abstract class.

A sub-class may **override** an operation defined by its parent class, which gives it a chance to handle requests instead of their parent classes. Class inheritance lets you define classes simply by extending other classes, making it easy to define families of objects having related functionality.

**Mixin class**: Class designed to provide an optional interface or functionality to other classes through inheritance (which promotes code reuse and modularity). It's not intended to be instantiated. It requires multiple inheritance.

<br>![mixin class](https://raw.githubusercontent.com/AnselmoGPP/Learn_Computer_Science/master/topics/software_development/resources/mixin_class.png)

**Object**:

- **Object’s class**: Defines how the object is implemented. It's the internal state and the implementation of its operations.
- **Object’s type**: The object’s interface (set of requests to which it can respond). An object can have many types, and objects of different classes can have the same type.

**Inheritance**:

- **Class inheritance**: Defines an object’s implementation in terms of another object’s implementation. Useful for extending an application’s functionality by reusing functionality in parent classes. It lets you define a new kind of object rapidly in terms of an old one.
- **Interface inheritance**: Defines when an object can be used in place of another. Polymorphism depends on this inheritance.

In C++, inheritance means both interface and implementation inheritance. The standard way to _inherit an interface_ in C++ is to inherit publicly from a class that has (pure) virtual member functions. In C++:

- Pure _interface inheritance_ can be approximately inheriting publicly from pure abstract classes.
- Pure implementation or _class inheritance_ can be approximated with private inheritance.

When inheritance is used carefully, all classes derived from an abstract class will share its interface. This implies that a subclass merely adds or overrides operations and doesn’t hide operations of the parent class. All subclasses can then respond to the requests in the interface of this abstract class, making them all subtypes of the abstract class. Benefits from manipulating objects solely in terms of the interface defined by abstract classes:

- Clients remain unaware of the specific types of objects they use, as long as the objects adhere to the interface that clients expect.
- Clients remain unaware of the classes that implement these objects. Clients only know about the abstract class/es defining the interface.

**Program to an interface, not an implementation**. Don’t declare variables to be instances of particular concrete classes. Instead, commit only to an interface defined by an abstract class. You have to instantiate concrete classes (i.e. specify a particular implementation) somewhere in your system, and the creational patterns let you do just that. By abstracting the process of object creation, these patterns give you different ways to associate an interface with its implementation transparently at instantiation. Creational patterns ensure that your system is written in terms of interfaces, not implementations.

### Reuse mechanisms

#### Most common techniques to compose behaviour in object-oriented systems

- **Class inheritance**:

You define the implementation of one class in terms of another’s. With inheritance, the internals of parent classes are often visible to subclasses (white-box reuse). Defined **statically** at compile-time (cannot change at run-time).

  - Advantages:

    - Straightforward to use because it’s supported directly by the programming language.
    - Easier to modify the implementation being reused.

  - Disadvantages:

    - You can’t change the implementations inherited from parent classes at run-time, because inheritance is defined at compile-time.
    - Inheritance exposes a subclass to details of its parent’s implementation (it’s often said that “inheritance breaks encapsulation”). The implementation of both a subclass and its parent class become so bound up that any change in the parent’s implementation will force the subclass to change.
    - If any aspect of the inherited implementation is not appropriate for new problems, the parent class must be rewritten/replaced. One solution: Inherit from abstract classes (they have little or no implementation)

- **Object composition**:

New functionality is obtained by assembling (composing) objects to get more complex functionality (it requires well-defined interfaces). No internal details of objects are visible (black-box reuse). It requires objects to respect each others’ interfaces (objects are accessed solely through their interfaces). Defined **dynamically** at run-time through objects acquiring references to objects.

  - Advantages:

    - It’s easy to compose behaviours at run-time by changing how they’re composed.
    - Any object can be replaced at run-time by another as long as it has same type.
    - Fewer implementation dependencies (since an object’s implementation is written in terms of objects interfaces).
    - Keeps each class encapsulated and focused on one task.
    - It has more objects (if fewer classes), and its behaviour depends on their relationships instead of being defined in one class.

  - Disadvantages:

    - It requires indirection, which can be less efficient.

**Favor object composition over class inheritance**: However, the set of available components is never quite rich enough in practice, so both mechanisms should work together. Inheritance makes it easier to make new components that can be composed with old ones. Object composition makes designs more reusable and simpler.

- **Delegation**:

It is a type of object composition that makes composition as powerful for reuse as inheritance. Two objects are involved in handling a request: a receiving object delegates operations to its **delegate** (analogous to subclasses deferring requests to parent classes). To let the delegated operation refer to the receiver, the receiver passes itself to the delegate. Delegation shows that inheritance can always be replaced with object composition.

Example: Instead of making class Window a subclass of Rectangle, Window class might keep a rectangle member variable and delegate Rectangle-specific behavior to it.

<br>![window object](https://raw.githubusercontent.com/AnselmoGPP/Learn_Computer_Science/master/topics/software_development/resources/delegation.png)

  - Advantages:

    - It’s easy to compose behaviors at run-time and change the way they’re composed. Replacing Rectangle instance with a Circle instance (assuming they have same type) our window can become circular at run-time.

  - Disadvantages:

    - Dynamic, highly parameterized software is harder to understand than more static software.
    - Run-time inefficiencies (though human inefficiencies are more important in the long run).

Delegation is a good choice only when it simplifies more than it complicates. It works best when used in highly stylized ways (i.e., in standard patterns). Several design patterns use delegation (State, Strategy, Visitor, Mediator, Chain of Responsability, Bridge).

- **Parameterized types (Templates)**:

It lets define types without specifying all the other types it uses. Unspecified types are supplied as parameters at the point of use (e.g.: a List class can be parameterized by the type of the elements it contains). It cannot change at run-time.

Example: To parameterize a sorting routine by the operation it uses to compare elements, we could make the comparison:

  1. an operation implemented by subclasses (Template method).
  2. the responsibility of an object that's passed to the sorting routine (Strategy).
  3. an argument of a template that specifies the name of the function to call to compare the elements.

#### Run-time and compile-time structures

**Aggregation** and **acquaintance** look similar but are different. They are determined more by intent than by explicit language mechanisms. 

- ** Aggregation** implies that one object owns or is responsible for another object. Both objects have identical lifetimes. Aggregation relationships tend to be fewer and more permanent than acquaintance. This is implemented with pointers or references, or by defining member variables that are real instances.

- **Acquaintance** implies that an object merely knows of another object. Acquainted objects may request operations of each other, but aren't responsible for each other. Acquaintance is a weaker relationship than aggregation and suggests much looser coupling between objects. Acquaintance relationships are made and remade more frequently (sometimes existing only for the duration of an operation), and are more dynamic. This is implemented with pointers or references.

Such disparity between a program's run-time and compile-time structures shows that code won't reveal everything about how a system will work. The system's run-time structure must be imposed more by the designer than the language. The relationships between objects and their types must be designed well because they determine how good or bad the run-time structure is.

Many design patterns capture the distinction between compile-time and run-time structures explicitly (Composite, Decorator, Observer, Chain of responsibility). In geeral, run-time structures aren't clear from the code until you understand the patterns.

#### Designing for change

To design a system robust to changes, you have to anticipate how the system might need to change over its lifetime. Otherwise, you risk major redesigns in the future, which is expensive. Design patterns ensure that a system can change in specific ways. Each design pattern lets some aspect of system structure to vary independently of other aspects. Some common causes of redesign are:

- Creating an object by specifying a class explicitly. This commits you to a particular implementation instead of a particular interface. Design patterns: Abstract factory, Factory method, Prototype.

- Dependence on specific operations. Specifying a particular operation commits you to one way of satisfying a request. Avoiding hard-coded requests makes it easier to change the way it gets satisfied both at compile-time and run-time. Design patterns: Chain, Command.

- Dependence on hardware and software platform. External OS interfaces and APIs are different on different hardware and software platforms. Limiting platform dependencies make your software will be easier to port and to keep up to date. Design patterns: Abstract factory, Bridge.

- Dependence on object representations or implementations. Hiding this information from clients prevent changes on these objects to cascade. Design patterns: Abstract factory, Bridge, Memento, Proxy.

- Algorithmic dependencies. Objects depending on an algorithm will have to change when the algorithm changes. Thus, isolate those algorithms that are likely to change. Design patterns: Builder, Iterator, Strategy, Template method, Visitor.

- Tight coupling. Classes tightly coupled are hard to reuse in isolation, leading to monolithic systems where you cannot change/remove a class without understanding and changing many others). This prevents a class from being used by itself, and make the code dense, and hard to learn, port, and maintain. Design patterns use some techniques (abstract coupling, layering...) to promote loosely coupled systems. Design patterns: Abstract factory, Bridge, Chain, Command, Facade, Mediator, Observer.

- Extending functionality by subclassing. This can lead to an explosion of subclasses. Object composition and delegation are flexible alternatives, though they could make designs harder to understand. Design patterns: Bridge, Chain, Composite, Decorator, Observer, Strategy.

- Inability to alter classes conveniently. Maybe you need the source code but it's not available, or maybe any change requires to modify many existing subclasses. Design patterns: Adapter, Decorator, Visitor.

Design patterns provide the flexibility your software needs, which depends on the types of software you build:

- **Application programs**: Internal reuse, maintainability, and extension are high priorities.

  - __Internal reuse__ ensures that you don't design and implement any more than you have to. Reducing dependencies (looser coupling) increase internal reuse. 
  - __Maintainability__ increases when limiting platform dependencies and layering a system.
  - __Extensibility__ is enhanced by reducing coupling, extending class hierarchies correctly, and exploiting object composition.

- **Toolkits**: Set of related and reusable classes designed to provide useful, general-purpose functionality. The doesn't impose a particular design on your application. They are used in many different applications, so they have to avoid assumptions and dependencies that can limit the toolkit's flexibility.

- **Frameworks**: Set of cooperating classes that make up a reusable design for a specific class of software (graphical editors, financial modelling, compilers...). You customize a framework to a particular application by creating application-specific subclasses of abstract classes from the framework. It dictates the architecture of your application (predefined by the framework). Frameworks enphasize design reuse over code reuse. The framework's architecture should work for all domain applications, so it should be as flexible and extensible as possible. Also, loose coupling is important to prevent minor changes to the framework to have major repercussions on the applications. Frameworks and design patterns are similar, but design patterns are more abstract, have smaller architectural elements, and are less specialized than frameworks.

### How to select a design pattern

- Consider how design patterns solve design problems. Find appropriate objects, determine their granularity, specify object interfaces, etc.
- Check the intent of each design pattern. 
- Study how patterns interrelate.
- Study patterns of like purpose. 
- Examine a cause of redesign.
- Consider what should be variable in your design without redesign. Encapsulate the concept that varies.

### How to use a design pattern

These are some guidelines, but you will develop your own way over time.

- Get an overview of the pattern, specially Applicability and Consecuences.
- Study the structure, participants, and collaborations (classes, objects, and their relationships).
- Study a sample code.
- Choose names for pattern participants that are meaningful in the application context and make the pattern more explicit in the implementation.
- Define the classes: Declare interfaces, establish inheritance relationships, define instance variables, identify existing classes that the pattern will affect, and modify them accordingly.
- Define application-specific names for operations in the pattern. Use the responsibilities and collaborations of each operation as a guide, be consistent in your naming conventions, and make the pattern explicit.
- Implement the operations to carry out the responsibilities and collaborations in the pattern. 
- Evaluate consequences of the pattern. They achieve flexibility and variability by introducing additional levels of indirection, which may complicate a design and/or cost some performance. Design patterns should only be applied where the flexibility they afford is actually needed.

<br>![modifiable design aspects](https://raw.githubusercontent.com/AnselmoGPP/Learn_Computer_Science/master/topics/software_development/resources/modifiable_design_aspects.png)


## Case study: Designing a document editor

We want to design a WYSIWYG document editor called Lexi. The user interface has a representation of the document, which can mix text and graphics freely in different formatting styles. It's surrounded by pull-down menus, scroll bars, and a some page icons for jumping to particular pages.

This will serve to learn about different design patterns: Composite, Strategy, Decorator.

### Design problems

- **Document structure**: The choice of internal representation for the document will impact the design of the rest of the application.
- **Formatting**: Arrangement of text and graphics into lines and columns. Formatting policies. Interaction between policies and the internal representation.
- **Embellishing the user interface**: Embellishments (scroll bars, borders, drop shadows…) should be able to be added and removed easily without affecting the rest of the application.
- **Supporting multiple look-and-feel standards**: Lexi should adapt easily to different look-and-feel standards (Motif, Presentation Manager...) without major modification.
- **Supporting multiple window systems**: Look-and-feel standards are usually implemented on different window systems. Lexi's design should be as independent of the window system as possible.
- **User operations**: User controls Lexi through various user interfaces (buttons, pull-down menus...). Their functionality is scattered throughout the objects in the application. Provide a uniform mechanism for both accessing this scattered functionality and for undoing its effects.
- **Analytical operations** (like spelling checking and hyphenation): Support for analytical operations (checking for misspelled words, determining hyphenation points...). Minimize the number of classes to modify to add a new analytical operation.

### Document structure

A document is an arrangement of basic graphical elements (characters, lines, polygons, and other shapes). An author often views them in terms of the document's physical structure (lines, columns, figures, tables, and other substructures). These structures have substructures of their own, and so on.

Lexi's user interface should let users manipulate these substructures directly (tables, diagrams...). The internal representation should support:

- Maintaining document's physical structure (i.e., arrangement of text and graphics into lines, columns, tables...).
- Generating and presenting the document visually.
- Mapping positions on the display to elements in the internal representation (useful when the user points to something).

Constraints:

- Text and graphics should be treated uniformly. The application's interface lets the user embed text within graphics freely and vice versa.
- Simple and complex elements should be treated uniformly. Our implementation shouldn't have to distinguish between single elements and groups of elements in the internal representation. However, when analysing text (for spelling errors, hyphenation points...), we do care about what the object is (we don't check the spelling of a polygon).

#### Recursive composition

**Recursive composition**: Common technique for representing hierarchically structured information. Increasingly complex elements are built out of simpler ones.

We can compose a document out of simple graphical elements. We can tile a set of characters and graphics from left to right to form a line, multiple lines can be arranged to form a column, multiple columns form a page, and so on.

- Composite (column)
  - Composite (row)
    - char R
    - char e
    - char d
    - space
    - car picture
  - Composite (row)
    - …

We can devote an object to each important element (characters, graphics, lines, columns...). The object structure mimics the document's physical structure, providing flexibility and extensibility. This implies that the objects need classes, and these classes need compatible interfaces, which is done through inheritance.

We define a **Glyph** abstract class for all objects that can appear in a document structure. Its subclasses define both primitive graphical (characters, images...) and structural elements (rows, columns...)

<br>![recursive composition](https://raw.githubusercontent.com/AnselmoGPP/Learn_Computer_Science/master/topics/software_development/resources/recursive_composition.png)

<br>![glyph structure](https://raw.githubusercontent.com/AnselmoGPP/Learn_Computer_Science/master/topics/software_development/resources/glyph.png)

Glyphs have 3 basic responsibilities: they know how to draw themselves, what space they occupy, and their children and parent

- `Draw(Window*)` operation: Glyph subclasses redefine it to render themselves onto a window. The `Window` class defines graphics operations for rendering text and basic shapes in a window on the screen. A `Rectangle` subclass of `Glyph` might redefine `Draw` as:

```
void Rectangle::Draw(Window *w) {
  w->DrawRect(_x0, _y0, _x1, _y1);
}
```

- `Bounds(Rect&)` operation: Glyph subclasses redefine it to return the rectangular area the glyph occupies. A parent glyph often needs to know how much space a child glyph occupies (for example, to arrange it with others in a line without overlapping).

- `Intersects(const Point&)` operation: It returns whether a specified point intersects the glyph. Used by Lexi to determined over which glyph or glyph structure the user clicked. The `Rectangle` class redefines it.

Glyphs have children (example: a `Row`'s children are the glyphs it arranges into a row), so we need a common interface to add (`Insert(Glyph *g, int index)`), remove (`Remove(Glyph *g)`), and access (`Child(int index)`) those children.

- `Child(int index)` operation returns the child, if any, at the given index. Glyphs like `Row` that have children should use `Child` internally instead of accessing the child data structure directly, so you won't have to modify operations like `Draw` that iterate through the children when you change the data structure used.

- `Parent` provides a standard interface to the glyph's parent, if any. Glyphs in Lexi store a reference to their parent, and their `Parent` operation simply returns this reference.

#### Composite pattern

Recursive composition is good for representing any potentially complex, hierarchical structure. The **Composite** pattern captures the essence of recursive composition in object-oriented terms.

### Formatting

Let's find out how to construct a physical structure for a properly formatted document. We will consider "formatting" as breaking a collection of glyphs into lines (linebreaking), but the next techniques apply equally well to breaking lines into columns, and columns into pages.

#### Encapsulating the formatting algorithm

There're many approaches to the formatting process, and there're many formatting algorithms (FAs) with different strengths and weaknesses. Since Lexi is a WYSIWYG editor, an important trade-off to consider is the balance between formatting quality and formatting speed. Another trade-off balances formatting speed and storage requirements (formatting time could be decreased by caching more information).

Because FAs tend to be complex, we could keep them independent of the document structure. Ideally, we could

- add new kinds of `Glyph` subclasses without regard to the FA.
- add new formatting algorithms without requiring to modify existing glyphs.
- easily change the FA at least at compile-time, if not at run-time as well.

We can get this by isolating the FA in an object. We will define a separate class hierarchy for objects that encapsulate FAs, where the hierarchy's root will define an interface supporting a wide range of FAs, and each subclass will implement the interface to carry out a particular algorithm. Then a Glyph subclass will structure its children automatically using a given algorithm object.

#### Compositor and Composition

A **Compositor** class will encapsulate a FA. The interface lets the compositor know what glyphs to format and when to do the formatting. The glyphs it formats are the children of a special `Glyph` subclass called **Composition**, which gets an instance of a Compositor subclass when it's created and tells it to `Compose` its glyphs when necessary. Each compositor subclass can implement a different FA.

<br>![compositor and composition](https://raw.githubusercontent.com/AnselmoGPP/Learn_Computer_Science/master/topics/software_development/resources/compositor_and_composition.png)

An unformatted Composition object (composite) contains only the visible glyphs, but doesn't contain glyphs that determine the document's physical structure (Row, Column...). When the composition needs formatting, it calls its compositor's `Compose` operation, which iterates through the composition's children and inserts new Row and Column glyphs according to the its FA. 

The Compositor-Composition class split ensures strong separation between code for the physical structure and code for different FAs. We can add new Compositor subclasses without touching the glyph classes, and vice versa. We can even change the FA at run-time by adding a single `SetCompositor` operation to Composition's basic glyph interface.

<br>![compositor generated glyphs](https://raw.githubusercontent.com/AnselmoGPP/Learn_Computer_Science/master/topics/software_development/resources/compositor.png)

#### Strategy pattern

The intent of the **Strategy pattern** is to encapsulate an algorithm in an object. The key participants in the pattern are **strategy objects** (they encapsulate different algorithms) (compositors are strategies), and the **context** in which they operate (composition is the context). The interfaces for the strategy and its context should be general enough to support a range of algorithms. You shouldn't have to change their interfaces to support a new algorithm.

In our example, the basic `Glyph` interface supports child access, insertion, and removal, which are operations general enough for Compositor to change the document's physical structure regardless of the FA used. Likewise, Compositor's interface gives Compositions whatever they need to initiate formatting.

### Embellishing the user interface

We consider 2 embellishments for Lexi's user interface (UI): a border around the text editing area, and a scroll bar for viewing different part of the page. To make it easy to add and remove them (especially at run-time), we shouldn't use inheritance to add them to the UI. We get the most flexibility if other UI objects don't know the embellishments are there.

#### Transparent enclosure

Embellishing the UI involves extending existing code. Using inheritance prevents us from rearranging embellishments at run-time, and also may result in an explosion of classes. We could add a border to Composition by subclassing it to yield a BorderedComposition class. Or maybe we want a ScrollableComposition. Or a BorderedScrollableComposition. We may end up with a class for every possible combination of embellishments, which becomes unworkable as the variety of embellishments grows.

Object composition offers a potentially more workable and flexible extension mechanism. We can make the embellishment itself an object (`Border`, `Scroll`...), not a subclass of Glyph. We can make the border contain the glyph, so the border-drawing code is kept entirely in the Border class, leaving other classes alone. Also, clients shouldn't care whether glyphs have borders or not, they should treat glyphs uniformly. Clients shouldn't have to treat the border containing the glyph any differently. They just tell it to draw itself as they told the plain glyph before. This implies that Border interface matches Glyph interface, so we subclass Border from Glyph to guarantee this relationship.

**Transparent enclosure**: It combines the notions of single-child (or single-component) composition and compatible interfaces. Clients generally cannot tell whether they're dealing with the component or its enclosure (i.e., the child's parent), especially if the enclosure simply delegates all its operations to its component. The enclosure can also augment the component's behaviour by doing work of its own before and/or after delegating an operation, and can also add state to the component.

#### Monoglyph

We can apply the concept of transparent enclosure to all glyphs that embellish other glyphs. We define a subclass of Glyph called **MonoGlyph** to serve as an abstract class for "embellishment glyphs". It stores a reference to a component and forwards all requests to it. It makes MonoGlyph totally transparent to clients by default. MonoGlyph subclasses reimplement `Draw`, which draws the glyph and then the embellishment.

<br>![MonoGlyph](https://raw.githubusercontent.com/AnselmoGPP/Learn_Computer_Science/master/topics/software_development/resources/monoglyph.png)

```
void MonoGlyph::Draw(Window* w) {
  _component->Draw(w);
}
```

```
void Border::Draw(Window* w) {
  MonoGlyph::Draw(w);
  DrawBorder(w);
}
```

`Border::Draw` extends the parent class operation to draw the border.

`Scroller` is a MonoGlyph that draws its component in different locations based on the positions of two scroll bars (embellishments). When it draws its component, it tells the graphics system to clip to its bounds. 

To add a border and a scrolling interface we compose the Composition instance in a Scroller instance, and compose this in a Border instance.

<br>![Embellished object structure](https://raw.githubusercontent.com/AnselmoGPP/Learn_Computer_Science/master/topics/software_development/resources/embellished_object_structure.png)

Reversing the order of composition, putting the bordered composition into the Scroller instance, would make the border be scrolled along with the text. Transparent enclosure makes it easy to experiment and keeps clients free of embellishment code. 

The border composes one glyph, not many, unlike compositions where parent objects can have arbitrarily many children. Putting a border around something means that "something" is singular. Keeping embellishment independent of other kinds of composition simplifies the embellishment classes, reduces their number, and prevents replicating existing composition functionality.

#### Decorator pattern

**Embellishment**: In the Decorator pattern, this refers to anything that adds responsibilities to an object.

**Decorator pattern**: It captures class and object relationships that support embellishment by transparent enclosure. Examples:

- Embellishing an abstract syntax tree with semantic actions.
- Finite state automaton with new transitions.
- Network of persistent objects with attribute tags.


### Supporting multiple look-and-feel standards

We want Lexi to be portable across hardware and software platforms. We should make porting as easy as possible. One obstacle is the diversity of **look-and-feel standards** (guidelines for how applications appear and react to the user, intended to enforce uniformity between applications). An application running on many platforms must conform to the UI style guide on each platform. We want Lexi to conform to multiple existing look-and-feel standards, make it easy to add new ones as they emerge, and support changing look-and-feel at run-time.

#### Abstracting object creation




64/378

<br>![glyph structure](https://raw.githubusercontent.com/AnselmoGPP/Learn_Computer_Science/master/topics/software_development/resources/glyph.png)
