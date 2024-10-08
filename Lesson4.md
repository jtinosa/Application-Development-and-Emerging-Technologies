# Design Patterns

In software engineering, design patterns are reusable solutions to commonly occurring problems in software design. These patterns started as best practices used in the industry and applied multiple times to similar problems encountered in different contexts. Design patterns are templates or blueprints that any developer can customize to solve recurring design problems. They are not specific pieces of code but general concepts for solving particular problems. These patterns are also used to design the architecture of an entire software system.

Design patterns are developed in the software industry. When a solution is repeatedly used in various projects, someone eventually puts a name to it and describes the solution in detail. That’s basically how a pattern gets discovered.

Design patterns are said to have four essential features:
- **Pattern Name**: The name of a pattern used to describe a design problem, its solution, and consequences.
- **Problem**: Describes when to use the pattern, explaining the problem and its context.
- **Solution**: Describes the elements that make up the design, their relationships, responsibilities, and collaborations. The pattern provides an abstract description of a design problem and how a general arrangement of elements solves it.
- **Consequences**: The results and interchanges of applying the pattern to the problem. They include time and space tradeoffs, flexibility, extensibility, and portability.

## Categories of Patterns

Design patterns differ by complexity, level of detail, and scale of applicability. There are three categories of design patterns in object-oriented design:
- **Creational Patterns**: These patterns deal with when and how objects are created. These provide object creation mechanisms that increase flexibility and reuse of existing codes.
- **Structural Patterns**: These describe how objects are composed into larger groups and explain how to assemble objects and classes into larger structures while keeping their structures flexible and efficient.
- **Behavioral Patterns**: These describe how responsibilities are distributed between objects in the design and how communication happens between objects.

## Creational Patterns

Creational design patterns are about class instantiation and deal with object creation mechanisms. There are five creational patterns:

### Singleton Pattern
This design pattern ensures a class has only one instance while providing a global access point to that instance.

- **Problem**: The Singleton pattern solves two problems:
  1. Ensures that a class has just a single instance, for example, to control access to a shared resource.
  2. Provides a global access point to that instance. However, this pattern may violate the Single Responsibility Principle.

- **Solution**: 
  1. Make the constructor private to prevent the creation of more instances.
  2. Create a static method that returns the singleton instance.

#### Structure of Singleton Pattern

![Singleton Structure](https://refactoring.guru/design-patterns/singleton)

### Factory Method Pattern
This provides an interface for creating objects in a superclass but allows subclasses to alter the type of object that will be created.

- **Problem**: Adding new types of transportation (e.g., sea logistics) requires changes to the entire codebase.
- **Solution**: The Factory Method pattern replaces direct object construction with calls to a factory method.

#### Structure of Factory Method Pattern

![Factory Method Structure](https://refactoring.guru/design-patterns/factory-method)

### Prototype Pattern
This pattern lets you copy existing objects without making the code dependent on their classes.

- **Problem**: Manually duplicating objects could result in unwanted coupling to their classes.
- **Solution**: The Prototype pattern delegates cloning to the objects being cloned.

#### Structure of Prototype Pattern

![Prototype Structure](https://refactoring.guru/design-patterns/prototype)

### Abstract Factory Pattern
Allows the creation of families of related objects without specifying their concrete classes.

- **Problem**: Creating individual objects in families (e.g., Modern furniture) requires specific object matching.
- **Solution**: Use abstract factory interfaces to create product families.

#### Structure of Abstract Factory Pattern

![Abstract Factory Structure](https://refactoring.guru/design-patterns/abstract-factory)

### Builder Pattern
Allows developers to construct complex objects step by step, enabling the creation of different types and representations using the same construction code.

- **Problem**: When creating objects requiring complex step-by-step initialization, the constructor can become overloaded.
- **Solution**: Use a builder object to organize construction into steps.

#### Structure of Builder Pattern

![Builder Pattern Structure](https://refactoring.guru/design-patterns/builder)

## Structural Patterns

Structural design patterns deal with the arrangement and relationship between classes in the software system. There are seven design patterns in this category:

### Adapter Pattern
Allows objects with incompatible interfaces to collaborate.

- **Problem**: A stock monitoring software uses XML data, but a new library requires JSON format.
- **Solution**: The adapter converts the interface of one object so that another object can understand it.

#### Structure of Adapter Pattern

![Adapter Structure](https://refactoring.guru/design-patterns/adapter)

### Bridge Pattern
This pattern allows developers to split a large class into two separate hierarchies, abstraction and implementation.

- **Problem**: Extending a shape class hierarchy for different types of shapes and colors leads to an exponential number of subclasses.
- **Solution**: Extract the color-related code into its own class hierarchy.

#### Structure of Bridge Pattern

![Bridge Structure](https://refactoring.guru/design-patterns/bridge)

### Composite Pattern
Allows developers to compose objects into tree structures and work with these structures as if they were individual objects.

- **Problem**: Calculating the total price of orders containing products and nested boxes is complex.
- **Solution**: Compose Products and Boxes using a common interface.

#### Structure of Composite Pattern

![Composite Structure](https://refactoring.guru/design-patterns/composite)

### Decorator Pattern
Allows developers to attach new behaviors to objects by placing these objects inside special wrapper objects.

- **Problem**: A notification library needs to support multiple types of notifications (e.g., email, SMS, social media).
- **Solution**: Use decorators to add new behaviors dynamically.

#### Structure of Decorator Pattern

![Decorator Structure](https://refactoring.guru/design-patterns/decorator)

### Facade Pattern
Provides a simplified interface to a complex set of classes.

- **Problem**: Working with complex libraries tightly couples your code to the library's implementation details.
- **Solution**: Use a facade to simplify interactions with the complex subsystem.

#### Structure of Facade Pattern

![Facade Structure](https://refactoring.guru/design-patterns/facade)

### Flyweight Pattern
Reduces memory usage by sharing parts of the object's state between multiple objects.

- **Problem**: A video game crashes due to memory exhaustion from representing too many particles.
- **Solution**: Separate the state-independent and state-dependent data.

#### Structure of Flyweight Pattern

![Flyweight Structure](https://refactoring.guru/design-patterns/flyweight)

### Proxy Pattern
Provides a placeholder or substitute for another object to control access to it.

- **Problem**: A large object consumes significant system resources but is only needed occasionally.
- **Solution**: The proxy creates the object when needed and delegates the work to it.

#### Structure of Proxy Pattern

![Proxy Structure](https://refactoring.guru/design-patterns/proxy)

## Behavioral Patterns

Behavioral design patterns are concerned with how objects communicate in a system. Some of the design patterns include Iterator, Observer, and Strategy design patterns.

### Iterator Pattern
Allows developers to traverse elements of a collection without exposing its underlying representation.

- **Problem**: Implementing different search algorithms could complicate the primary responsibilities of the collection class.
- **Solution**: Use iterators to encapsulate traversal details.

#### Structure of Iterator Pattern

![Iterator Structure](https://refactoring.guru/design-patterns/iterator)

### Observer Pattern
Defines a subscription mechanism to notify multiple objects of any events that happen to the object being observed.

- **Problem**: A store needs to notify customers when new products are available, but not all customers are interested.
- **Solution**: Implement a subscription system where customers subscribe to specific product notifications.

#### Structure of Observer Pattern

![Observer Structure](https://refactoring.guru/design-patterns/observer)

### Strategy Pattern
Allows developers to define a family of algorithms, put them into separate classes, and make them interchangeable.

- **Problem**: A navigation application grows complex as more route planning algorithms are added.
- **Solution**: Use strategies to separate algorithms into different classes.

#### Structure of Strategy Pattern

![Strategy Structure](https://refactoring.guru/design-patterns/strategy)
