# Diagrams

## Table of Contents
+ [References](#references)
+ [Introduction](#introduction)
+ [Class diagrams](#class-diagrams)
+ [Object diagrams](#object-diagrams)
+ [Interaction diagrams](#interaction-diagrams)


## References
- Erich Gamma, Richard Helm, Ralph Johnson, John Vlissides (1994) _**Design patterns. Elements of object-oriented software**_. Addison-Wesley. Retrieved from [link1](http://www.uml.org.cn/c++/pdf/designpatterns.pdf), [link2](http://www.grch.com.ar/docs/unlu.poo/Gamma-DesignPatternsIntro.pdf), [link3](https://github.com/TushaarGVS/Design-Patterns-Mentorship/blob/master/Erich%20Gamma%2C%20Richard%20Helm%2C%20Ralph%20Johnson%2C%20John%20M.%20Vlissides-Design%20Patterns_%20Elements%20of%20Reusable%20Object-Oriented%20Software%20%20-Addison-Wesley%20Professional%20(1994).pdf).


## Introduction

Diagrams are a formal notation for denoting relationships and interactions between classes and objects. The following diagrams represent **classes**, **objects**, and **interactions**. 

The class and object diagrams are based on **OMT (Object Modeling Technique)** [RBP<sup>+</sup>91, Rum94]. The interaction diagrams are taken from **Objectory** [JCJO92] and the **Booch method** [Boo94].


## Class diagrams

It depicts classes, their structure, and the static relationships between them.

- A **class** is denoted by a box. The class name in bold type is at the top. Below are the key operations. And below are instance variables. Type information is optional. Italic type is used for abstract classes or operations.

- **Participant classes** (they're involved in the design pattern in a certain role) are shown in black. **Client classes** (they use or interact with a design pattern to solve a problem) are shown in gray. 

- **Class inheritance**: Triangle connecting a subclass to its parent class.

- **Object reference** representing a part-of or aggregation relationship: Arrowheaded line, pointing to the class that's aggregated, with a diamond base. **Acquaintance** is indicated by an arrowheaded line without diamond base. The reference name may appear near the base to distinguish it from other references.

- Which classes instantiate which others: Dashed arrowheaded line pointing to the instantiated class.

- **Operations implementation** can be sketched using a dashed line with circle base.

<br>![class_diagrams](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/class_diagrams.png)


## Object diagrams

It depicts a particular object structure at run-time. It shows instances exclusively (a snapshot of them).

- A **rounded box** denotes an object. A line separates the object name from any object references.

- Objects are named "aSomething" (`aDrawing`, `anObject`...), where "Something" is the class of the object.

- Arrows indicate the object referenced.

<br>![object_diagrams](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/object_diagrams.png)


## Interaction diagrams

It shows the flow of requests between objects, the order in which requests between objects get executed.

- **Time** flights from top to bottom.

- **Lifetime** of a particular object: Solid vertical line. If it has not been instantiated yet, it's a dashed vertical line.

- **Active object** (i.e., it's handling a request): Vertical rectangle.

- Requests sent to other objects: Horizontal arrow pointing to the receiving object. A request to the sending object points back to the sender. The name of the request is shown above the arrow. 

- Request to create an object: Dashed arrowheaded line.
 
Example: `aCreationTool` requests to create `aLineShape`. Then, `aLineShape` is added to `aDrawing`, which prompts `aDrawing` to send a `Refresh` request to itself (`aDrawing` sends a `Draw` request to `aLineShape` as part of the `Refresh` operation). 

<br>![interaction_diagrams](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/interaction_diagrams.png)


