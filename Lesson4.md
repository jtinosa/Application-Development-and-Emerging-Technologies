# Design Patterns

**Design Patterns** are reusable solutions for common problems in software design. They are not actual code but rather concepts for solving issues in system architecture.

### Key Features of a Design Pattern:
1. **Pattern Name**: A unique identifier for the design problem.
2. **Problem**: When to use the pattern.
3. **Solution**: The structure of elements and their relationships.
4. **Consequences**: The outcomes of using the pattern.

### Categories of Design Patterns:
1. **Creational Patterns**: Manage object creation.
2. **Structural Patterns**: Deal with the structure and composition of objects.
3. **Behavioral Patterns**: Handle communication between objects.

## Creational Design Patterns
### **Singleton Design Pattern**

#### **Definition:**
The Singleton Pattern ensures that a class has only one instance and provides a global point of access to that instance. This pattern restricts the instantiation of a class to one object and is often used when exactly one object is needed to coordinate actions across a system.

#### **Problem:**
Use the Singleton Pattern when:
- You need exactly one instance of a class to control a critical resource or manage system-wide coordination.
- You want to prevent multiple instances of a class from being created (e.g., logging services, configuration managers, or connection pools).

#### **Solution:**
The Singleton Pattern ensures that only one instance of the class is created by:
1. Making the constructor private so the class cannot be instantiated from outside.
2. Creating a static method that returns the sole instance of the class.
3. Storing the single instance of the class as a static member.

**Class Structure**:
- **Singleton**: The class itself, which ensures only one instance exists and provides a method to retrieve that instance.

**UML Structure**:
```
+--------------+
|  Singleton   |
+--------------+
| -instance    |
| +getInstance()|
+--------------+
```

#### **Example Code:**
Here’s a simple example in Java:

```java
// Singleton class
class Singleton {
    // Static variable to hold the single instance
    private static Singleton instance;

    // Private constructor to prevent instantiation
    private Singleton() {
        // Initialization code (if any)
    }

    // Static method to return the single instance
    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }

    public void showMessage() {
        System.out.println("Singleton Instance: Hello World!");
    }
}

// Usage
public class SingletonPatternExample {
    public static void main(String[] args) {
        // Get the only instance of Singleton
        Singleton singleton = Singleton.getInstance();

        // Show a message from the singleton instance
        singleton.showMessage();
    }
}
```

#### **Consequences:**

- **Positive**:
  - **Controlled access to the sole instance**: Only one instance of the class is created, ensuring controlled access to critical resources (e.g., configurations, logging).
  - **Global point of access**: The single instance is accessible globally, making it easier to manage.
  - **Lazy instantiation**: The Singleton can be initialized only when it is first requested, which may improve resource efficiency.

- **Negative**:
  - **Difficult to test**: Singleton classes can be hard to test in isolation, especially in multithreaded environments, because they introduce a global state.
  - **Potential for misuse**: Singleton can be overused and lead to a tightly coupled system, especially when developers use it as a global variable.
  - **Thread safety concerns**: In multithreaded scenarios, careful handling (e.g., using synchronization or double-checked locking) is required to ensure that only one instance is created.

### **Factory Method Design Pattern**

#### **Definition:**
The Factory Method Pattern defines an interface for creating an object, but lets subclasses alter the type of objects that will be created. It provides a way to delegate the instantiation logic to child classes, promoting loose coupling.

#### **Problem:**
Use the Factory Method Pattern when:
- You want to decouple the client code from the object creation logic, allowing the class to defer instantiation to subclasses.
- You need flexibility in creating different types of objects, but the exact type of object isn't known until runtime.
- You want to follow the "open-closed principle" where adding new products doesn’t require modifying existing code.

#### **Solution:**
The Factory Method Pattern relies on:
1. **Creator (Factory)**: Defines the factory method, which returns an instance of a product.
2. **Product**: Defines the interface of the object to be created.
3. **ConcreteCreator**: Implements the factory method to return an instance of the concrete product.

**Class Structure**:
- **Creator**: Declares the factory method.
- **ConcreteCreator**: Overrides the factory method to create a concrete product.
- **Product**: Interface or abstract class defining the product.
- **ConcreteProduct**: Concrete implementations of the product.

**UML Structure**:
```
+-------------------+               +-------------------+
|   Creator         |               |   Product         |
+-------------------+               +-------------------+
| +factoryMethod()  |               |                   |
+-------------------+               +-------------------+
        ^                                   ^
        |                                   |
+-------------------+               +-------------------+
| ConcreteCreator   |               | ConcreteProduct   |
+-------------------+               +-------------------+
| +factoryMethod()  |               |                   |
+-------------------+               +-------------------+
```

#### **Example Code:**
Here’s an example in Java:

```java
// Product Interface
interface Product {
    void use();
}

// ConcreteProductA Class
class ConcreteProductA implements Product {
    public void use() {
        System.out.println("Using Product A");
    }
}

// ConcreteProductB Class
class ConcreteProductB implements Product {
    public void use() {
        System.out.println("Using Product B");
    }
}

// Creator Class (Factory)
abstract class Creator {
    public abstract Product factoryMethod();

    public void someOperation() {
        Product product = factoryMethod();
        product.use();
    }
}

// ConcreteCreatorA Class
class ConcreteCreatorA extends Creator {
    public Product factoryMethod() {
        return new ConcreteProductA();
    }
}

// ConcreteCreatorB Class
class ConcreteCreatorB extends Creator {
    public Product factoryMethod() {
        return new ConcreteProductB();
    }
}

// Usage
public class FactoryMethodExample {
    public static void main(String[] args) {
        Creator creatorA = new ConcreteCreatorA();
        creatorA.someOperation();  // Outputs: Using Product A

        Creator creatorB = new ConcreteCreatorB();
        creatorB.someOperation();  // Outputs: Using Product B
    }
}
```

#### **Consequences:**

- **Positive**:
  - **Loose coupling**: Clients don’t need to know the specific class of objects they use, only the interface or abstract class.
  - **Single Responsibility**: The factory method isolates the object creation code, allowing it to be easily changed without impacting the rest of the code.
  - **Open-Closed Principle**: It’s easy to add new types of products without modifying existing code by introducing new concrete creators.

- **Negative**:
  - **Increased complexity**: For simple applications, using a factory method might add unnecessary complexity as you have to introduce additional classes and interfaces.
  - **Multiple subclasses**: Overuse can lead to a proliferation of subclasses and make the code harder to maintain.

### **Prototype Design Pattern**

#### **Definition:**
The Prototype Pattern is a creational design pattern that allows an object to create a copy of itself, known as a prototype. This pattern is used when the cost of creating a new instance of an object is more expensive than copying an existing instance. It provides a way to create new objects by copying an existing object, thus facilitating object creation without coupling to specific classes.

#### **Problem:**
Use the Prototype Pattern when:
- You want to avoid the overhead of creating an object from scratch, especially when the object is complex.
- You need to create an object dynamically at runtime based on an existing object.
- You want to share an object that serves as a template for other objects, allowing new instances to be created with similar properties.

#### **Solution:**
The Prototype Pattern involves:
1. **Prototype Interface**: Declares the cloning method.
2. **ConcretePrototype**: Implements the prototype interface and provides the actual cloning functionality.
3. **Client**: Uses the prototype to create new instances without knowing their concrete classes.

**Class Structure**:
- **Prototype**: Interface or abstract class with a method for cloning.
- **ConcretePrototype**: Concrete classes that implement the prototype interface.
- **Client**: The class that uses the prototype to create new objects.

**UML Structure**:
```
+-------------------+
|     Prototype     |
+-------------------+
| +clone()          |
+-------------------+
        ^
        |
+-------------------+
| ConcretePrototype  |
+-------------------+
| +clone()          |
+-------------------+
```

#### **Example Code:**
Here’s an example in Java:

```java
// Prototype Interface
interface Prototype {
    Prototype clone();
}

// ConcretePrototype Class
class ConcretePrototype implements Prototype {
    private String property;

    public ConcretePrototype(String property) {
        this.property = property;
    }

    // Implementing the clone method
    @Override
    public Prototype clone() {
        return new ConcretePrototype(this.property);
    }

    public String getProperty() {
        return property;
    }
}

// Client Code
public class PrototypePatternExample {
    public static void main(String[] args) {
        // Create a new ConcretePrototype instance
        ConcretePrototype original = new ConcretePrototype("Original Property");

        // Clone the original object
        ConcretePrototype clone = (ConcretePrototype) original.clone();

        // Display properties
        System.out.println("Original: " + original.getProperty()); // Outputs: Original: Original Property
        System.out.println("Clone: " + clone.getProperty());       // Outputs: Clone: Original Property
    }
}
```

#### **Consequences:**

- **Positive**:
  - **Dynamic object creation**: New objects can be created at runtime without specifying their concrete class.
  - **Reduced subclassing**: It helps in avoiding class proliferation, as new objects can be created from existing ones.
  - **Flexibility**: The prototype can be modified, and clones can have different configurations or states.

- **Negative**:
  - **Complexity**: Implementing the cloning logic may add complexity to the codebase, especially if the objects have deep hierarchies or contain mutable fields.
  - **Inconsistency**: If the prototype isn't properly designed, it can lead to inconsistencies between the prototype and its clones, especially if they share mutable states.
  - **Performance overhead**: Cloning large objects can still incur performance costs, particularly if they contain significant amounts of data.

4. **Abstract Factory Pattern**:
   - Produces families of related objects without specifying concrete classes.
   - **Example**: Creating modern or Victorian furniture sets.

5. **Builder Pattern**:
   - Constructs complex objects step by step.
   - **Example**: Building a house with different parts like walls, doors, windows.

## Structural Design Patterns

1. **Adapter Pattern**:
   - Converts one interface into another, making incompatible interfaces work together.
   - **Example**: Adapting XML data to work with a JSON-based library.

2. **Bridge Pattern**:
   - Separates abstraction from implementation, allowing both to vary independently.
   - **Example**: Handling multiple shapes and colors without creating a class for every combination.

3. **Composite Pattern**:
   - Composes objects into tree structures to treat individual and composite objects uniformly.
   - **Example**: Orders with products and boxes that can contain other boxes or products.

4. **Decorator Pattern**:
   - Adds new functionality to an object by wrapping it in a class that implements the same interface.
   - **Example**: Adding SMS and email notifications dynamically.

5. **Facade Pattern**:
   - Simplifies interactions with a complex subsystem by providing a unified interface.
   - **Example**: A single interface for interacting with a complex library.

6. **Flyweight Pattern**:
   - Reduces memory usage by sharing common data between objects.
   - **Example**: Multiple bullets in a game sharing the same attributes.

7. **Proxy Pattern**:
   - Provides a placeholder for another object to control access to it.
   - **Example**: Loading a large object only when needed.

## Behavioral Design Patterns

1. **Iterator Pattern**:
   - Provides a way to access elements of a collection without exposing its underlying structure.
   - **Example**: Traversing a list or tree structure.

2. **Observer Pattern**:
   - Notifies multiple objects about changes to a subject.
   - **Example**: A store notifying customers about new product arrivals.

3. **Strategy Pattern**:
   - Defines a family of algorithms and allows them to be interchangeable.
   - **Example**: Different algorithms for calculating routes in a navigation app.
