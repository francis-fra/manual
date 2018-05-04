### Abstraction
* abstract data type (classes)


### encapsulation
* hide implementation from users (other object)
* internal implementation can be changed without affecting the user interface
* modular structure - identify what changes and seperate from what stays the same


### polymorphism
* same implementation can be applied to different and related (inherited) objects
* code the interface, not implementation
* program to a supertype - generalize the concept

### inheritance
* code reuse (maintence and extensible)
* changes can be applied to related objects
* enforce is-a relationship
* more structured concept

### Principles

1. encapsulate what varies
* favor composition over inheritance
    * let you change behaviour at runtime
    * inheritance bind behavior statically
    * composition bind behavior dynamically at run time

2. program to interface not implementation
3. classes should be open for extension, but closed for modification
    * classes can be easily extended without modifying existing codes
    * reduces impact and prevents classes (modular design) from changes made by other components
4. Dependency Inversion Principles
    * Depend upon abstractions, not concrete classes
    * depends on higher level class means higher flexibility for extension
    * no variable should hold a reference to a concree class
    * no class should be derived from a concrete class
    * no method should override an implementation of any of its base classes

5. Principle of Least Knowledge
    * when building a large number of classes coupled together, chnages in one part
    * cascade to other parts
    * A lot of depdencies results a fragile system which is costly to maintain

6. Hollywood Principle
    * Don't call us, we'll call you

7. Design principle
    * A class should have only one reason to change

### Design Patterns

###### Strategy
defines a family of algorithms, encasulates each one and make them
interchangeable. Strategy lets the algorithm vary independently from clients
than use it

###### Decorator
attach additional capabilities to existing class dynamically
flexible alternative to subclassing for extending functionality

###### Factory
defines an interface for creating objects
defer instantiation to the subclass (inheritance)
encapsulates the creator class, decoupled with the product class

###### Abstract Factory
create families of related or dependent objects without specifying their concrete classes
it creates families of products independent on the concrete class
the client is decoupled from (without knowing) the concrete products
it relies on object composition rather than inheritance

###### Singleton
ensure that a class has only one instance and provide global access to it

###### Command
encapsulate a request as an object, thereby letting you parameterize other
objects with different requests, queue or log requests and support undoable operations.

###### Adaptor
converts the interface of a class into another

###### Facade
provides a unified inerface to a set of interfaces in a subsystem.
defined a higher level interface

###### Template
defines the skeleton of an algorithm, deferring some steps to subclasses.
It lets the subcless redefine the steps without changing the algorithm's structure.

###### Iterator
provides a way to access the elemtns of an aggregate object without
exposing its underlying representation

###### Composite
allows you to compose objects into tree structures to represent
part-whole hierarchies

###### State
allows an object to alter its behavior when its internal state changes
think of state pattern as an alternative to putting lots of conditionals
think of strategy pattern as an alternative to subclassing (inheritance)

###### Proxy
provides a surrogate or placeholder for another object ot nctorl access to it
