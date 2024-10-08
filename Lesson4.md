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

### **Abstract Factory Design Pattern**

#### **Definition:**
The Abstract Factory Pattern is a creational design pattern that provides an interface for creating families of related or dependent objects without specifying their concrete classes. This pattern is used to encapsulate a group of individual factories that have a common theme, allowing clients to create objects in a way that is independent of their specific classes.

#### **Problem:**
Use the Abstract Factory Pattern when:
- You want to create a system that is independent of how its objects are created, composed, and represented.
- You need to ensure that products from a specific family are used together (e.g., GUI components that should match in style).
- You want to provide a client with a way to configure an object without specifying the concrete classes used.

#### **Solution:**
The Abstract Factory Pattern consists of:
1. **AbstractFactory**: Declares the creation methods for each type of product.
2. **ConcreteFactory**: Implements the creation methods to produce specific products.
3. **AbstractProduct**: Defines the interface for a type of product.
4. **ConcreteProduct**: Implements the product interface.

**Class Structure**:
- **AbstractFactory**: Declares creation methods for various abstract products.
- **ConcreteFactory**: Implements the creation methods for specific products.
- **AbstractProduct**: Interface for products created by the factories.
- **ConcreteProduct**: Implementations of the abstract products.

**UML Structure**:
```
+-------------------+          +-------------------+
|   AbstractFactory  |<------->|   AbstractProduct  |
+-------------------+          +-------------------+
| +createProductA() |          |                   |
| +createProductB() |          +-------------------+
+-------------------+                   ^
        ^                               |
        |                               |
+-------------------+          +-------------------+
| ConcreteFactoryA  |          | ConcreteProductA   |
+-------------------+          +-------------------+
| +createProductA() |          |                   |
| +createProductB() |          +-------------------+
+-------------------+                   ^
        ^                               |
        |                               |
+-------------------+          +-------------------+
| ConcreteFactoryB  |          | ConcreteProductB   |
+-------------------+          +-------------------+
| +createProductA() |          |                   |
| +createProductB() |          +-------------------+
+-------------------+
```

#### **Example Code:**
Here’s an example in Java:

```java
// AbstractProductA
interface ProductA {
    void use();
}

// AbstractProductB
interface ProductB {
    void use();
}

// ConcreteProductA1
class ConcreteProductA1 implements ProductA {
    public void use() {
        System.out.println("Using Product A1");
    }
}

// ConcreteProductA2
class ConcreteProductA2 implements ProductA {
    public void use() {
        System.out.println("Using Product A2");
    }
}

// ConcreteProductB1
class ConcreteProductB1 implements ProductB {
    public void use() {
        System.out.println("Using Product B1");
    }
}

// ConcreteProductB2
class ConcreteProductB2 implements ProductB {
    public void use() {
        System.out.println("Using Product B2");
    }
}

// AbstractFactory
interface AbstractFactory {
    ProductA createProductA();
    ProductB createProductB();
}

// ConcreteFactory1
class ConcreteFactory1 implements AbstractFactory {
    public ProductA createProductA() {
        return new ConcreteProductA1();
    }

    public ProductB createProductB() {
        return new ConcreteProductB1();
    }
}

// ConcreteFactory2
class ConcreteFactory2 implements AbstractFactory {
    public ProductA createProductA() {
        return new ConcreteProductA2();
    }

    public ProductB createProductB() {
        return new ConcreteProductB2();
    }
}

// Client Code
public class AbstractFactoryExample {
    public static void main(String[] args) {
        AbstractFactory factory1 = new ConcreteFactory1();
        ProductA productA1 = factory1.createProductA();
        ProductB productB1 = factory1.createProductB();
        productA1.use(); // Outputs: Using Product A1
        productB1.use(); // Outputs: Using Product B1

        AbstractFactory factory2 = new ConcreteFactory2();
        ProductA productA2 = factory2.createProductA();
        ProductB productB2 = factory2.createProductB();
        productA2.use(); // Outputs: Using Product A2
        productB2.use(); // Outputs: Using Product B2
    }
}
```

#### **Consequences:**

- **Positive**:
  - **Encapsulation of object creation**: Clients don’t need to know the details of how objects are created or how they are composed.
  - **Consistency among products**: Ensures that products from the same family are compatible and can be used together seamlessly.
  - **Easier to introduce new products**: Adding new concrete factories for new product families does not affect existing code.

- **Negative**:
  - **Increased complexity**: The system can become overly complex with multiple interfaces and classes, making it harder to understand.
  - **Difficulties in extending the pattern**: If there are many variations of products, extending the abstract factory to accommodate new product variations may require significant changes.
  - **Potential for code bloat**: If many product families are required, it may lead to a proliferation of classes and interfaces.


### **Builder Design Pattern**

#### **Definition:**
The Builder Pattern is a creational design pattern that allows for the step-by-step construction of complex objects. It separates the construction of a complex object from its representation, enabling the same construction process to create different representations. This pattern is particularly useful when an object needs to be created with many optional parameters or when the object creation process involves multiple steps.

#### **Problem:**
Use the Builder Pattern when:
- You want to create an object that requires many parameters, especially when some of those parameters are optional.
- The construction process of the object is complex and involves multiple steps.
- You want to avoid a telescoping constructor (a constructor with many parameters) that can lead to confusion and difficulty in maintaining the code.

#### **Solution:**
The Builder Pattern consists of:
1. **Builder Interface**: Defines the methods for creating parts of the complex object.
2. **ConcreteBuilder**: Implements the builder interface and provides specific implementations for constructing the parts of the object.
3. **Director**: Responsible for managing the construction process, calling the builder methods in a specific order.
4. **Product**: The complex object that is being constructed.

**Class Structure**:
- **Builder**: Interface for building parts of the product.
- **ConcreteBuilder**: Implements the builder interface to create specific product representations.
- **Director**: Uses a builder instance to construct the product.
- **Product**: Represents the complex object that is built.

**UML Structure**:
```
+------------------+
|      Director    |
+------------------+
| +construct()     |
+------------------+
        |
        v
+------------------+
|      Builder     |
+------------------+
| +buildPart()     |
| +getResult()     |
+------------------+
        ^
        |
+------------------+
|  ConcreteBuilder  |
+------------------+
| +buildPart()     |
| +getResult()     |
+------------------+
        |
        v
+------------------+
|      Product     |
+------------------+
|                  |
+------------------+
```

#### **Example Code:**
Here’s an example in Java:

```java
// Product Class
class Product {
    private String partA;
    private String partB;
    private String partC;

    // Getters
    public String getPartA() { return partA; }
    public String getPartB() { return partB; }
    public String getPartC() { return partC; }

    // Builder Class
    public static class Builder {
        private String partA;
        private String partB;
        private String partC;

        public Builder setPartA(String partA) {
            this.partA = partA;
            return this;
        }

        public Builder setPartB(String partB) {
            this.partB = partB;
            return this;
        }

        public Builder setPartC(String partC) {
            this.partC = partC;
            return this;
        }

        public Product build() {
            Product product = new Product();
            product.partA = this.partA;
            product.partB = this.partB;
            product.partC = this.partC;
            return product;
        }
    }
}

// Client Code
public class BuilderPatternExample {
    public static void main(String[] args) {
        Product product = new Product.Builder()
                .setPartA("Part A")
                .setPartB("Part B")
                .setPartC("Part C")
                .build();

        // Displaying product parts
        System.out.println("Product Parts:");
        System.out.println("A: " + product.getPartA());
        System.out.println("B: " + product.getPartB());
        System.out.println("C: " + product.getPartC());
    }
}
```

#### **Consequences:**

- **Positive**:
  - **Improved readability**: The code becomes easier to read and understand, especially when constructing complex objects.
  - **Flexibility**: It allows for varying representations of an object without changing the code that uses it.
  - **Encapsulation**: It encapsulates the construction logic, making it easier to manage.

- **Negative**:
  - **Increased complexity**: It may introduce additional classes and interfaces, making the system more complex.
  - **Overhead**: In cases where simple objects are created, using a builder can introduce unnecessary overhead.

## Structural Design Patterns

### **Adapter Design Pattern**

#### **Definition:**
The Adapter Pattern is a structural design pattern that allows incompatible interfaces to work together. It acts as a bridge between two incompatible interfaces, enabling them to communicate and function as if they were compatible. This pattern is useful when you want to use an existing class but its interface does not match the one you need.

#### **Problem:**
Use the Adapter Pattern when:
- You want to integrate a class from a library or framework that does not match the interface you need.
- You want to use multiple classes with different interfaces interchangeably.
- You need to adapt an interface to match a specific client without modifying the existing code.

#### **Solution:**
The Adapter Pattern consists of:
1. **Target**: The interface that clients use.
2. **Adapter**: The class that implements the target interface and translates calls to the adaptee.
3. **Adaptee**: The existing class with an incompatible interface that needs adapting.
4. **Client**: The code that interacts with the target interface.

**Class Structure**:
- **Target**: Defines the domain-specific interface that the client uses.
- **Adapter**: Implements the target interface and adapts the adaptee interface to it.
- **Adaptee**: Contains the existing functionality that needs to be adapted.

**UML Structure**:
```
+-------------------+
|      Client       |
+-------------------+
|                   |
+-------------------+
        |
        v
+-------------------+
|      Target       |
+-------------------+
| +request()        |
+-------------------+
        ^
        |
+-------------------+
|      Adapter      |
+-------------------+
| -adaptee         |
| +request()       |
+-------------------+
        |
        v
+-------------------+
|     Adaptee       |
+-------------------+
| +specificRequest()|
+-------------------+
```

#### **Example Code:**
Here’s an example in Java:

```java
// Target Interface
interface Target {
    void request();
}

// Adaptee Class
class Adaptee {
    public void specificRequest() {
        System.out.println("Called specificRequest from Adaptee.");
    }
}

// Adapter Class
class Adapter implements Target {
    private Adaptee adaptee;

    public Adapter(Adaptee adaptee) {
        this.adaptee = adaptee;
    }

    @Override
    public void request() {
        System.out.println("Adapter converts the request.");
        adaptee.specificRequest();
    }
}

// Client Code
public class AdapterPatternExample {
    public static void main(String[] args) {
        Adaptee adaptee = new Adaptee();
        Target target = new Adapter(adaptee);
        target.request();  // Outputs: Adapter converts the request. Called specificRequest from Adaptee.
    }
}
```

#### **Consequences:**

- **Positive**:
  - **Increased flexibility**: It allows for the integration of new classes into existing systems without modifying the existing code.
  - **Code reusability**: Enables the reuse of existing code that has an incompatible interface.
  - **Decoupling**: Reduces dependencies between classes, making the codebase easier to manage and extend.

- **Negative**:
  - **Complexity**: It can add an extra layer of abstraction, which may complicate the code structure.
  - **Overhead**: If overused, it can lead to increased complexity and maintenance challenges.


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
