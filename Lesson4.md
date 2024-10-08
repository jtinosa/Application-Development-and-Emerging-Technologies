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

1. **Singleton Pattern**:
   - Ensures a class has only one instance and provides global access to it.
   - **Example**: Database connections where only one connection object is required.

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
