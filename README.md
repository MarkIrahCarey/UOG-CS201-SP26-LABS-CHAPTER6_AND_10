# Lab 6: Design with Functions and Classes

These labs focus on **designing modular and reusable code** using functions and object-oriented programming with classes. You will apply concepts from Chapters 6 and 10, including top-down design, recursion, namespaces, higher-order functions, default arguments, and class design.

The goal is to practice breaking down problems into well-structured functions and modeling real-world entities using classes.

## Chapter 6 & 10: Summary of Key Concepts

### Design with Functions (Chapter 6)
- **Functions as Abstractions** — Hide complexity and eliminate code redundancy
- **Top-down Design** — Break large problems into smaller, manageable functions (stepwise refinement)
- **Recursion** — Functions that call themselves with a base case and recursive step
- **Namespaces & Scope** — Understanding module variables, parameters, and temporary variables
- **Default Arguments** — Creating flexible functions with optional parameters
- **Higher-order Functions** — Using `map()`, `filter()`, `reduce()`, and `lambda` functions
- **Jump Tables** — Using dictionaries to store and call functions

### Design with Classes (Chapter 10)
- **Classes** as blueprints for creating objects
- **Instance variables** for storing object state
- **`__init__`** constructor and **`__str__`** method
- **Accessors** (getters) vs **Mutators** (setters)
- **Class variables** shared across all instances
- **Operator Overloading** (`__add__`, `__eq__`, `__lt__`, etc.)
- **Inheritance** and the `super()` function
- **Polymorphism** — Same method name with different behaviors in subclasses

### Why We Use Functions and Classes
- Functions support **divide and conquer** and improve code reusability
- Classes allow us to model entities that have both **data** and **behavior**
- Together they lead to clean, maintainable, and extensible programs

## Grading Criteria

Documentation and good design are major components of your grade. Clear docstrings, logical function decomposition, proper class structure, and use of OOP principles will be evaluated carefully.

| Lab   | Description                                      | Comments / Documentation | Functionality | Total |
|-------|--------------------------------------------------|---------------------------|---------------|-------|
| Lab6a | Recursion with the Lucas Numbers                 | 5pts                     | 10pts        | 15pts |
| Lab6b | Coffee Machine Class                             | 10pts                    | 25pts        | 35pts |
| Lab6c | Player Class (RPG Level Up, Items & Combat)      | 15pts                    | 35pts        | 50pts |
| **Total** |                                              | **30pts**                | **70pts**    | **100pts** |
