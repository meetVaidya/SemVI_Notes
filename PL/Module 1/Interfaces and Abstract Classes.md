
### Interfaces

In Java, an **interface** defines a contract for what a class can do, without dictating how it must do it.  
- It can contain abstract method declarations, static methods, default methods (from Java 8), and constants.
- Interfaces enable abstraction and support multiple inheritance, **unlike classes**. 
- A class that implements an interface must provide concrete implementations for all its abstract methods.
- **Functional interfaces** have exactly one abstract method and can be used as targets for lambda expressions.

*Example:*  
```java
public interface Animal {
    void makeSound(); // abstract method
    default void eat() { System.out.println("Eating..."); } // default method
    static void sleep() { System.out.println("Sleeping..."); } // static method
}
```

### Abstract Classes

An **abstract class** is a class that cannot be instantiated directly and is meant to be subclassed.
- It may contain a mix of abstract methods (without implementation) and concrete methods (with implementation).
- Abstract classes can have constructors, fields, and methods just like regular classes.
- Subclasses must implement all abstract methods or themselves be declared abstract.

*Example:*  
```java
public abstract class Animal {
    public abstract void makeSound(); // Abstract method
    public void eat() { System.out.println("Eating..."); } // Concrete method
}
```

#### Key differences between interfaces and abstract classes:
- Interfaces cannot have instance fields or constructors; abstract classes can.
- A class can implement multiple interfaces but can extend only one class (abstract or not).
- Starting from Java 8, interfaces can have default and static methods, but cannot have constructors or state.