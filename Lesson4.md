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

2. **Factory Method Pattern**:
   - Defines an interface for creating objects, but lets subclasses decide which class to instantiate.
   - **Example**: Logistics app creating trucks or ships based on the need.

3. **Prototype Pattern**:
   - Allows copying an object without depending on its class.
   - **Example**: Cloning an object without knowing its specific class.

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
