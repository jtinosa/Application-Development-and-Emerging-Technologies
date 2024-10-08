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

### **Bridge Design Pattern**

#### **Definition:**
The Bridge Pattern is a structural design pattern that separates an abstraction from its implementation, allowing the two to vary independently. This pattern is useful when both the abstractions and implementations can change, and it promotes loose coupling between them.

#### **Problem:**
Use the Bridge Pattern when:
- You need to separate the interface from its implementation to allow for flexible variations.
- You have multiple implementations for a class, and you want to avoid a large number of subclasses for every combination of abstraction and implementation.
- You want to decouple the abstraction from the implementation to enhance code maintainability and readability.

#### **Solution:**
The Bridge Pattern consists of:
1. **Abstraction**: Defines the abstraction and maintains a reference to the implementer.
2. **RefinedAbstraction**: Extends the abstraction, allowing for additional behavior.
3. **Implementer**: Defines the interface for implementation classes.
4. **ConcreteImplementer**: Implements the specific functionalities defined in the implementer interface.

**Class Structure**:
- **Abstraction**: Interface or abstract class for the higher-level operations.
- **RefinedAbstraction**: Concrete implementation of the abstraction that may add additional features.
- **Implementer**: Interface for the implementation classes.
- **ConcreteImplementer**: Concrete classes implementing the implementer interface.

**UML Structure**:
```
+------------------+
|   Abstraction     |
+------------------+
| -implementer     |
| +operation()     |
+------------------+
        |
        v
+------------------+
| RefinedAbstraction|
+------------------+
| +operation()     |
+------------------+
        |
        v
+------------------+
|   Implementer    |
+------------------+
| +operationImpl() |
+------------------+
        ^
        |
+------------------+
| ConcreteImplementer|
+------------------+
| +operationImpl() |
+------------------+
```

#### **Example Code:**
Here’s an example in Java:

```java
// Implementer Interface
interface DrawingAPI {
    void drawCircle(double x, double y, double radius);
}

// ConcreteImplementer Class
class DrawingAPI1 implements DrawingAPI {
    @Override
    public void drawCircle(double x, double y, double radius) {
        System.out.println("API1.circle at " + x + ":" + y + " radius " + radius);
    }
}

class DrawingAPI2 implements DrawingAPI {
    @Override
    public void drawCircle(double x, double y, double radius) {
        System.out.println("API2.circle at " + x + ":" + y + " radius " + radius);
    }
}

// Abstraction Class
abstract class Shape {
    protected DrawingAPI drawingAPI;

    protected Shape(DrawingAPI drawingAPI) {
        this.drawingAPI = drawingAPI;
    }

    public abstract void draw(); // High-level abstraction
}

// RefinedAbstraction Class
class Circle extends Shape {
    private double x, y, radius;

    public Circle(double x, double y, double radius, DrawingAPI drawingAPI) {
        super(drawingAPI);
        this.x = x;
        this.y = y;
        this.radius = radius;
    }

    @Override
    public void draw() {
        drawingAPI.drawCircle(x, y, radius); // Delegation to implementer
    }
}

// Client Code
public class BridgePatternExample {
    public static void main(String[] args) {
        Shape circle1 = new Circle(5, 10, 2, new DrawingAPI1());
        Shape circle2 = new Circle(10, 20, 3, new DrawingAPI2());

        circle1.draw(); // Outputs: API1.circle at 5:10 radius 2
        circle2.draw(); // Outputs: API2.circle at 10:20 radius 3
    }
}
```

#### **Consequences:**

- **Positive**:
  - **Flexibility**: Allows for changing both the abstraction and the implementation independently, promoting better code maintenance.
  - **Reduced class explosion**: Minimizes the number of classes by separating the interface from the implementation.
  - **Enhanced code organization**: Improves the organization of code by decoupling components.

- **Negative**:
  - **Increased complexity**: The added layer of abstraction can make the system more complex and harder to understand.
  - **Difficulties in tracing calls**: The additional layers can lead to more difficulty in tracing calls through the system.

### **Composite Design Pattern**

#### **Definition:**
The Composite Pattern is a structural design pattern that allows you to compose objects into tree structures to represent part-whole hierarchies. This pattern lets clients treat individual objects and compositions of objects uniformly. It is particularly useful for building complex user interfaces and hierarchical data structures.

#### **Problem:**
Use the Composite Pattern when:
- You need to represent a part-whole hierarchy of objects.
- You want clients to be able to treat individual objects and compositions of objects uniformly.
- You need to simplify the client code that works with tree structures, enabling it to interact with both individual objects and groups of objects in the same way.

#### **Solution:**
The Composite Pattern consists of:
1. **Component**: An interface or abstract class that defines the common interface for both the leaf nodes and the composite nodes.
2. **Leaf**: Represents the leaf nodes in the tree structure that do not have children.
3. **Composite**: Represents the composite nodes that can have children and implements the component interface.

**Class Structure**:
- **Component**: Interface or abstract class for the objects in the composition.
- **Leaf**: Concrete implementation of the component that represents leaf nodes.
- **Composite**: Concrete implementation of the component that can hold other components.

**UML Structure**:
```
+------------------+
|    Component      |
+------------------+
| +operation()     |
+------------------+
        ^
        |
+------------------+
|      Leaf        |
+------------------+
| +operation()     |
+------------------+
        ^
        |
+------------------+
|    Composite     |
+------------------+
| -children        |
| +operation()     |
| +add()           |
| +remove()        |
| +getChild()      |
+------------------+
```

#### **Example Code:**
Here’s an example in Java:

```java
import java.util.ArrayList;
import java.util.List;

// Component Interface
interface Graphic {
    void draw();
}

// Leaf Class
class Circle implements Graphic {
    @Override
    public void draw() {
        System.out.println("Drawing a Circle.");
    }
}

// Leaf Class
class Square implements Graphic {
    @Override
    public void draw() {
        System.out.println("Drawing a Square.");
    }
}

// Composite Class
class CompositeGraphic implements Graphic {
    private List<Graphic> graphics = new ArrayList<>();

    public void add(Graphic graphic) {
        graphics.add(graphic);
    }

    public void remove(Graphic graphic) {
        graphics.remove(graphic);
    }

    @Override
    public void draw() {
        for (Graphic graphic : graphics) {
            graphic.draw(); // Delegating drawing to child components
        }
    }
}

// Client Code
public class CompositePatternExample {
    public static void main(String[] args) {
        Graphic circle1 = new Circle();
        Graphic circle2 = new Circle();
        Graphic square = new Square();

        CompositeGraphic compositeGraphic = new CompositeGraphic();
        compositeGraphic.add(circle1);
        compositeGraphic.add(circle2);
        compositeGraphic.add(square);

        // Draw the composite graphic
        compositeGraphic.draw(); // Outputs: Drawing a Circle. Drawing a Circle. Drawing a Square.
    }
}
```

#### **Consequences:**

- **Positive**:
  - **Simplified client code**: Clients can work with complex hierarchies without needing to understand the details of the underlying structure.
  - **Flexibility**: It is easy to add new components to the system, either as leaf nodes or composite nodes.
  - **Uniformity**: Clients can treat both leaf nodes and composite nodes uniformly, simplifying the interface.

- **Negative**:
  - **Increased complexity**: The structure can become complicated, and clients may end up managing a large number of objects.
  - **Performance issues**: In large tree structures, operations on composites can become inefficient due to the overhead of managing many child components.

### **Decorator Design Pattern**

#### **Definition:**
The Decorator Pattern is a structural design pattern that allows behavior to be added to individual objects, either statically or dynamically, without affecting the behavior of other objects from the same class. This pattern is useful for adhering to the Single Responsibility Principle by allowing functionality to be divided among classes with unique concerns.

#### **Problem:**
Use the Decorator Pattern when:
- You want to add responsibilities to individual objects dynamically and transparently, without affecting other objects.
- You need to extend the functionality of classes in a flexible and reusable way.
- You want to avoid a large number of subclasses for every possible combination of behaviors.

#### **Solution:**
The Decorator Pattern consists of:
1. **Component**: An interface or abstract class defining the operations that can be decorated.
2. **ConcreteComponent**: The original object that can be decorated.
3. **Decorator**: An abstract class that implements the component interface and holds a reference to a component. It can add behavior before or after delegating calls to the component.
4. **ConcreteDecorator**: A class that extends the decorator and adds specific functionality.

**Class Structure**:
- **Component**: Interface for the objects that can have responsibilities added to them.
- **ConcreteComponent**: The object being decorated.
- **Decorator**: Abstract class implementing the component interface and containing a reference to a component.
- **ConcreteDecorator**: Extends the decorator to add additional behavior.

**UML Structure**:
```
+------------------+
|    Component      |
+------------------+
| +operation()     |
+------------------+
        ^
        |
+------------------+
| ConcreteComponent |
+------------------+
| +operation()     |
+------------------+
        ^
        |
+------------------+
|    Decorator     |
+------------------+
| -component       |
| +operation()     |
+------------------+
        ^
        |
+------------------+
| ConcreteDecorator |
+------------------+
| +operation()     |
+------------------+
```

#### **Example Code:**
Here’s an example in Java:

```java
// Component Interface
interface Coffee {
    String getDescription();
    double cost();
}

// ConcreteComponent Class
class SimpleCoffee implements Coffee {
    @Override
    public String getDescription() {
        return "Simple coffee";
    }

    @Override
    public double cost() {
        return 5.00;
    }
}

// Decorator Class
abstract class CoffeeDecorator implements Coffee {
    protected Coffee coffee;

    public CoffeeDecorator(Coffee coffee) {
        this.coffee = coffee;
    }
}

// ConcreteDecorator Class
class MilkDecorator extends CoffeeDecorator {
    public MilkDecorator(Coffee coffee) {
        super(coffee);
    }

    @Override
    public String getDescription() {
        return coffee.getDescription() + ", milk";
    }

    @Override
    public double cost() {
        return coffee.cost() + 1.00; // Adds cost of milk
    }
}

// ConcreteDecorator Class
class SugarDecorator extends CoffeeDecorator {
    public SugarDecorator(Coffee coffee) {
        super(coffee);
    }

    @Override
    public String getDescription() {
        return coffee.getDescription() + ", sugar";
    }

    @Override
    public double cost() {
        return coffee.cost() + 0.50; // Adds cost of sugar
    }
}

// Client Code
public class DecoratorPatternExample {
    public static void main(String[] args) {
        Coffee coffee = new SimpleCoffee();
        System.out.println(coffee.getDescription() + " $" + coffee.cost());

        coffee = new MilkDecorator(coffee);
        System.out.println(coffee.getDescription() + " $" + coffee.cost());

        coffee = new SugarDecorator(coffee);
        System.out.println(coffee.getDescription() + " $" + coffee.cost());
    }
}
```

#### **Consequences:**

- **Positive**:
  - **Flexibility**: You can mix and match decorators to create different combinations of behavior.
  - **Single Responsibility Principle**: Each decorator can focus on a specific behavior, keeping the code modular and maintainable.
  - **Open/Closed Principle**: The pattern allows new functionality to be added without modifying existing code.

- **Negative**:
  - **Complexity**: The system can become complicated with many decorators, making it harder to understand and maintain.
  - **Performance Overhead**: Each decorator adds a layer of indirection, which can impact performance, especially if used extensively.

### **Facade Design Pattern**

#### **Definition:**
The Facade Pattern is a structural design pattern that provides a simplified interface to a complex subsystem or a set of interfaces. It defines a higher-level interface that makes the subsystem easier to use, helping to reduce dependencies between the client and the subsystem.

#### **Problem:**
Use the Facade Pattern when:
- You want to provide a simple interface to a complex subsystem.
- You want to hide the complexity of the subsystem from the client code.
- You need to decouple the client code from the subsystem, reducing the number of classes that the client needs to interact with.

#### **Solution:**
The Facade Pattern consists of:
1. **Facade**: A class that provides a simplified interface to a complex subsystem.
2. **Subsystem Classes**: The classes that are part of the complex subsystem, which may have multiple interfaces.

**Class Structure**:
- **Facade**: The interface for the client to interact with.
- **Subsystem Classes**: Individual classes that implement the complex functionality.

**UML Structure**:
```
+------------------+
|      Facade      |
+------------------+
| +operation()     |
+------------------+
        |
        |
+------------------+        +------------------+
|  SubsystemClass1 |        |  SubsystemClass2 |
+------------------+        +------------------+
| +operation1()    |        | +operation2()    |
+------------------+        +------------------+
```

#### **Example Code:**
Here’s an example in Java:

```java
// Subsystem Class 1
class SubsystemA {
    public void operationA() {
        System.out.println("Subsystem A: Operation A");
    }
}

// Subsystem Class 2
class SubsystemB {
    public void operationB() {
        System.out.println("Subsystem B: Operation B");
    }
}

// Facade Class
class Facade {
    private SubsystemA subsystemA;
    private SubsystemB subsystemB;

    public Facade() {
        this.subsystemA = new SubsystemA();
        this.subsystemB = new SubsystemB();
    }

    public void simpleOperation() {
        subsystemA.operationA();
        subsystemB.operationB();
    }
}

// Client Code
public class FacadePatternExample {
    public static void main(String[] args) {
        Facade facade = new Facade();
        facade.simpleOperation();
    }
}
```

#### **Consequences:**

- **Positive**:
  - **Simplified Interface**: Provides a simplified interface for the client, making it easier to interact with the subsystem.
  - **Reduced Dependencies**: Clients are less dependent on the complex subsystem, leading to a more maintainable codebase.
  - **Encapsulation**: Hides the complexity of the subsystem, promoting better organization and separation of concerns.

- **Negative**:
  - **Potential for Over-Simplification**: The facade might become too simplistic, potentially hiding useful functionality in the subsystem that clients may need.
  - **Single Point of Failure**: If the facade class changes or fails, it can impact all clients that rely on it, potentially leading to a lack of flexibility.

### **Flyweight Design Pattern**

#### **Definition:**
The Flyweight Pattern is a structural design pattern that reduces the memory usage of an application by sharing common parts of state between multiple objects. It is used to optimize the use of memory in situations where a large number of similar objects are created, allowing for a more efficient use of resources.

#### **Problem:**
Use the Flyweight Pattern when:
- You need to create a large number of objects that share similar state or behavior.
- The overhead of storing these objects individually would consume too much memory.
- You want to minimize the memory footprint of your application while maintaining performance.

#### **Solution:**
The Flyweight Pattern consists of:
1. **Flyweight**: An interface or abstract class that defines the common interface for all shared objects.
2. **ConcreteFlyweight**: A class that implements the Flyweight interface and holds the intrinsic state (shared state) of the objects.
3. **FlyweightFactory**: A class responsible for creating and managing the Flyweight objects, ensuring that they are shared appropriately.
4. **Client**: The code that uses the Flyweight objects, providing the extrinsic state (non-shared state) as needed.

**Class Structure**:
- **Flyweight**: Interface for shared objects.
- **ConcreteFlyweight**: Implements the Flyweight interface.
- **FlyweightFactory**: Manages Flyweight instances.

**UML Structure**:
```
+------------------+
|     Flyweight     |
+------------------+
| +operation()     |
+------------------+
        ^
        |
+------------------+
| ConcreteFlyweight |
+------------------+
| +operation()     |
+------------------+
        ^
        |
+------------------+
| FlyweightFactory  |
+------------------+
| +getFlyweight()   |
+------------------+
```

#### **Example Code:**
Here’s an example in Java:

```java
import java.util.HashMap;
import java.util.Map;

// Flyweight Interface
interface TreeType {
    void display(int x, int y);
}

// ConcreteFlyweight Class
class Tree implements TreeType {
    private String name;
    private String color;

    public Tree(String name, String color) {
        this.name = name;
        this.color = color;
    }

    @Override
    public void display(int x, int y) {
        System.out.println("Tree: " + name + ", Color: " + color + " at (" + x + ", " + y + ")");
    }
}

// FlyweightFactory Class
class TreeFactory {
    private Map<String, TreeType> trees = new HashMap<>();

    public TreeType getTree(String name, String color) {
        String key = name + "-" + color;
        if (!trees.containsKey(key)) {
            trees.put(key, new Tree(name, color));
        }
        return trees.get(key);
    }
}

// Client Code
public class FlyweightPatternExample {
    public static void main(String[] args) {
        TreeFactory treeFactory = new TreeFactory();

        TreeType tree1 = treeFactory.getTree("Oak", "Green");
        tree1.display(1, 2);

        TreeType tree2 = treeFactory.getTree("Pine", "Dark Green");
        tree2.display(3, 4);

        TreeType tree3 = treeFactory.getTree("Oak", "Green");
        tree3.display(5, 6); // Reuses the Oak tree object

        // Check if the same object is reused
        System.out.println("Are tree1 and tree3 the same object? " + (tree1 == tree3));
    }
}
```

#### **Consequences:**

- **Positive**:
  - **Memory Efficiency**: Significantly reduces memory usage by sharing common states among objects.
  - **Performance Improvement**: Faster creation of objects by reusing existing instances.
  - **Flexibility**: You can easily add new flyweight objects without affecting the existing system.

- **Negative**:
  - **Complexity**: Increases system complexity, as it requires careful management of shared and non-shared states.
  - **Difficulty in Maintenance**: The shared state can make it more challenging to understand the behavior of individual objects, especially if there are many variations of the shared state.

### **Proxy Design Pattern**

#### **Definition:**
The Proxy Pattern is a structural design pattern that provides a surrogate or placeholder for another object to control access to it. This pattern allows you to create a proxy object that can represent another object, enabling functionalities such as lazy initialization, access control, logging, and more.

#### **Problem:**
Use the Proxy Pattern when:
- You need to control access to an object, such as restricting access based on certain criteria.
- You want to add additional behavior (like logging or caching) when accessing an object.
- You need to implement lazy initialization for a resource-heavy object, deferring its creation until it's actually needed.

#### **Solution:**
The Proxy Pattern consists of:
1. **Subject**: An interface or abstract class defining the operations that can be performed on the real object.
2. **RealSubject**: The actual object that the proxy represents and controls access to.
3. **Proxy**: A class that implements the Subject interface and contains a reference to the RealSubject. The proxy delegates requests to the real object and can add additional behavior.

**Class Structure**:
- **Subject**: The interface for the RealSubject and Proxy.
- **RealSubject**: The actual implementation of the Subject interface.
- **Proxy**: Implements the Subject interface and controls access to the RealSubject.

**UML Structure**:
```
+------------------+
|     Subject      |
+------------------+
| +request()       |
+------------------+
        ^
        |
+------------------+
|  RealSubject     |
+------------------+
| +request()       |
+------------------+
        ^
        |
+------------------+
|      Proxy       |
+------------------+
| -realSubject     |
| +request()       |
+------------------+
```

#### **Example Code:**
Here’s an example in Java:

```java
// Subject Interface
interface Image {
    void display();
}

// RealSubject Class
class RealImage implements Image {
    private String filename;

    public RealImage(String filename) {
        this.filename = filename;
        loadImageFromDisk(); // Simulate heavy loading
    }

    private void loadImageFromDisk() {
        System.out.println("Loading " + filename);
    }

    @Override
    public void display() {
        System.out.println("Displaying " + filename);
    }
}

// Proxy Class
class ProxyImage implements Image {
    private RealImage realImage;
    private String filename;

    public ProxyImage(String filename) {
        this.filename = filename;
    }

    @Override
    public void display() {
        if (realImage == null) {
            realImage = new RealImage(filename); // Lazy initialization
        }
        realImage.display();
    }
}

// Client Code
public class ProxyPatternExample {
    public static void main(String[] args) {
        Image image1 = new ProxyImage("image1.jpg");
        Image image2 = new ProxyImage("image2.jpg");

        // The image is loaded and displayed
        image1.display();
        
        // The image is displayed without reloading
        image1.display();
        
        // The image is loaded and displayed
        image2.display();
    }
}
```

#### **Consequences:**

- **Positive**:
  - **Access Control**: The proxy can provide control over access to the real object, allowing for security and authorization checks.
  - **Lazy Initialization**: It can delay the creation of the real object until it is actually needed, saving resources.
  - **Additional Functionality**: You can add extra features such as logging, caching, or monitoring without modifying the real object.

- **Negative**:
  - **Complexity**: Adds additional layers of abstraction, which can complicate the design and make it harder to understand.
  - **Performance Overhead**: Depending on the proxy's implementation, it may introduce performance overhead due to additional indirection.

## Behavioral Design Patterns

### **Iterator Design Pattern**

#### **Definition:**
The Iterator Pattern is a behavioral design pattern that provides a way to access the elements of a collection object sequentially without exposing its underlying representation. It allows for traversing different data structures with a common interface, promoting decoupling between the collection and the traversal mechanism.

#### **Problem:**
Use the Iterator Pattern when:
- You need to traverse a collection of objects without exposing its internal structure.
- You want to provide a uniform interface for traversing different types of collections.
- You want to allow multiple traversals of a collection simultaneously.

#### **Solution:**
The Iterator Pattern consists of:
1. **Iterator**: An interface that defines methods for iterating over a collection (e.g., `next()`, `hasNext()`).
2. **ConcreteIterator**: A class that implements the Iterator interface and keeps track of the current position in the collection.
3. **Aggregate**: An interface that defines a method for creating an iterator.
4. **ConcreteAggregate**: A class that implements the Aggregate interface and returns an instance of the ConcreteIterator.

**Class Structure**:
- **Iterator**: Interface for iteration.
- **ConcreteIterator**: Implements the Iterator interface.
- **Aggregate**: Interface for collection.
- **ConcreteAggregate**: Implements the Aggregate interface.

**UML Structure**:
```
+------------------+
|     Iterator     |
+------------------+
| +next()          |
| +hasNext()       |
+------------------+
        ^
        |
+------------------+
| ConcreteIterator  |
+------------------+
| -collection      |
| -currentIndex    |
| +next()          |
| +hasNext()       |
+------------------+
        ^
        |
+------------------+
|    Aggregate      |
+------------------+
| +createIterator() |
+------------------+
        ^
        |
+------------------+
| ConcreteAggregate |
+------------------+
| +createIterator() |
+------------------+
```

#### **Example Code:**
Here’s an example in Java:

```java
import java.util.ArrayList;
import java.util.List;

// Iterator Interface
interface Iterator {
    boolean hasNext();
    Object next();
}

// Aggregate Interface
interface Aggregate {
    Iterator createIterator();
}

// Concrete Iterator Class
class ConcreteIterator implements Iterator {
    private List<Object> items;
    private int currentIndex = 0;

    public ConcreteIterator(List<Object> items) {
        this.items = items;
    }

    @Override
    public boolean hasNext() {
        return currentIndex < items.size();
    }

    @Override
    public Object next() {
        if (this.hasNext()) {
            return items.get(currentIndex++);
        }
        return null;
    }
}

// Concrete Aggregate Class
class ConcreteAggregate implements Aggregate {
    private List<Object> items = new ArrayList<>();

    public void addItem(Object item) {
        items.add(item);
    }

    @Override
    public Iterator createIterator() {
        return new ConcreteIterator(items);
    }
}

// Client Code
public class IteratorPatternExample {
    public static void main(String[] args) {
        ConcreteAggregate aggregate = new ConcreteAggregate();
        aggregate.addItem("Item 1");
        aggregate.addItem("Item 2");
        aggregate.addItem("Item 3");

        Iterator iterator = aggregate.createIterator();
        while (iterator.hasNext()) {
            System.out.println(iterator.next());
        }
    }
}
```

#### **Consequences:**

- **Positive**:
  - **Decoupling**: Separates the responsibility of traversing a collection from the collection itself, promoting clean code.
  - **Uniformity**: Provides a common interface for traversing different types of collections.
  - **Flexibility**: You can create multiple iterators for the same collection, allowing for concurrent iterations.

- **Negative**:
  - **Complexity**: Introduces additional classes and interfaces, which can complicate the design.
  - **Performance Overhead**: The iteration may incur some performance overhead, especially if there are many levels of indirection.


2. **Observer Pattern**:
   - Notifies multiple objects about changes to a subject.
   - **Example**: A store notifying customers about new product arrivals.

3. **Strategy Pattern**:
   - Defines a family of algorithms and allows them to be interchangeable.
   - **Example**: Different algorithms for calculating routes in a navigation app.
