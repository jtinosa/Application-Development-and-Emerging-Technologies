# Design Principles and Patterns

---

## Overview of Design Principles

- Software design occurs during the design phase of development.
- Changes in requirements can lead to changes in the source code.
- A bad software architecture has three main issues:
  - **Rigidity**: Hard to change because one change affects many parts.
  - **Fragility**: Changes cause unexpected software breakages.
  - **Immobility**: Modules are hard to reuse in other systems.

---

## SOLID Principles

**SOLID** is a set of five principles introduced by Robert Martin and grouped into an acronym by Michael Feathers. These principles are aimed at improving software design and maintainability.

### S: Single Responsibility Principle (SRP)
- A module or class should only have one reason to change.
- Example of violation: An `Employee` class that handles payroll, reporting, and saving data.

---

### O: Open-Closed Principle (OCP)
- Classes should be open for extension but closed for modification.
- Example of violation: A `BankAccount` class that needs modification each time a new account type is added.
- Solution: Use inheritance or interfaces to extend class behavior without changing the existing class.

---

### L: Liskov Substitution Principle (LSP)
- Derived classes should be substitutable for their base classes.
- Example: `License` and its derived classes `PersonalLicense` and `BusinessLicense`, which can be used interchangeably without breaking functionality.

---

### I: Interface Segregation Principle (ISP)
- Avoid forcing clients to depend on methods they don’t use.
- Example of violation: A payment interface that requires credit card validation even for cash transactions.
- Solution: Split the interface into smaller, more specific interfaces.

---

### D: Dependency Inversion Principle (DIP)
- High-level modules should not depend on low-level modules. Both should depend on abstractions.
- Example: The `UserManager` class depends on the `EmailNotifier` class.
- Solution: Use an interface (e.g., `INotifier`) to decouple high-level classes from low-level details.

---

## Summary

Following the SOLID principles helps to:
- Reduce complexity.
- Improve readability, extensibility, and maintainability.
- Simplify testing and reusability.

---
