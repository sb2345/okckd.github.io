---
layout: post
title: "[Java OOP] Interface and Abstract classes "
comments: true
category: Java OOP

---

### Overview

[source](http://www.programmerinterview.com/index.php/java-questions/interface-vs-abstract-class/)

__A class__ must be declared abstract when it has one or more __abstract methods__.

__An interface__ differs from an abstract class because an interface is not a class. An interface is essentially a type that __can be satisfied by any class__ that implements the interface. 

### Abstract classes: strong relationship

__Abstract classes__ are meant to be inherited from, and often __indicates a strong relationship__.

For instance, if we have an abstract base class called "Canine", any deriving class should be an animal that belongs to the Canine family (like a Dog or a Wolf). 

__With an interface on the other hand__, the relationship is __not necessarily strong__. 

For example, if we have a class called "House", that class could also implement an interface called "AirConditioning". Having air conditioning not an essential part of a House. 

__A TownHouse__ is a type of House, that relationship is very strong, and would be more appropriately defined __through inheritance__ instead of interfaces.

### What's more

1. Multiple inheritance

    Java class can inherit from only one abstract class, but can implement multiple interfaces.

1. Abstract method 

    Abstract class can have non-abstract methods with actual implementation details. 

### When to use which

__Use abstract class when__: 

1. You want to __[share code](http://docs.oracle.com/javase/tutorial/java/IandI/abstract.html)__ among several closely related classes.

1. you want to be able to declare __non-public members__. In an interface, all methods must be public.

1. you think you will need to __add methods__ in the future. 

    Because if you add new method headings to an interface, then all of the classes that already implement that interface will have to be changed to implement the new methods. That can be quite a hassle.

__Use interface when__: 

1. You expect that __unrelated classes__ would implement your interface. For example, the interfaces __Comparable and Cloneable__ are implemented by many unrelated classes. 

1. you think that the API will not change for a while.

1. you want to have something similar to multiple inheritance.
