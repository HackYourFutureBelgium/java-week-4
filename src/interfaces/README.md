# 🔌 Interfaces in Java

An **interface** in Java is a **contract** that defines methods a class must implement.  
It provides **abstraction** and supports **multiple inheritance of type**.

---

## ✨ Key Points

- Declared with the `interface` keyword.  
- Can contain:  
  - **abstract methods** (default before Java 8).  
  - **default methods** (Java 8+, with a body).  
  - **static methods** (Java 8+).  
  - **private methods** (Java 9+).
  - **constants** (implicitly `public static final`).  
- A class implements an interface using the `implements` keyword.  
- A class can implement **multiple interfaces**.  

---

## ✅ Example 1 – Basic Interface

```java
package week4.interfaces;

interface Animal 
{
    void makeSound(); // abstract method

    // default method
    default void sleep() 
    { 
        System.out.println("Zzz...");
    }
    
    static void info() 
    { // static method
        System.out.println("Animals are living beings.");
        
        // Calling private method from static method
        privateMethod();
    }
    
    private void privateMethod() 
    { 
        System.out.println("This is a private method inside the interface.");
    }
}

class Dog implements Animal 
{
    @Override
    public void makeSound() {
        System.out.println("Woof!");
    }
}

public class InterfaceDemo 
{
    public static void main(String[] args) 
    {
        Animal a = new Dog();
        a.makeSound(); // Woof!
    }
}
````

---

## ⚖️ Interface vs Abstract Class

### 🔑 Key Differences

| Feature                  | **Interface**                                           | **Abstract Class**                                                   |
|--------------------------|---------------------------------------------------------|----------------------------------------------------------------------|
| **Keyword**              | `interface`                                             | `abstract class`                                                     |
| **Multiple inheritance** | ✅ A class can implement many interfaces                 | ❌ Can only extend one abstract class                                 |
| **Methods**              | Abstract (default), plus `default` & `static` (Java 8+) | Both abstract + concrete (normal) methods                            |
| **Fields**               | Implicitly `public static final` (constants)            | Instance variables allowed (any access level, mutable)               |
| **Constructors**         | ❌ Not allowed                                           | ✅ Allowed (to initialize fields)                                     |
| **When to use**          | Define a **contract/ability** (`Flyable`, `Swimmable`)  | Provide a **base class** with shared state/logic (`Animal`, `Shape`) |

---

## ✨ When to Use Interfaces

* To define a **contract** (what a class can do).
* When **unrelated classes** should share abilities.
* When you need **multiple inheritance of type** (since Java doesn’t support multiple class inheritance).

👉 Example:

* `class Bird implements Flyable`
* `class Plane implements Flyable`
  Different things, same ability → both can `fly()`.

---

## ✨ When to Use Abstract Classes

* When classes are **closely related**.
* When they share **state (fields)** and **behavior (methods)**.
* When you want to provide a **common base** but allow subclasses to override.

👉 Example:

* `abstract class Animal { abstract void makeSound(); }`
* `class Dog extends Animal { void makeSound() { System.out.println("Woof"); } }`

---

## ✅ Example – Interface + Abstract Class Together

```java
// Interface = ability
interface Flyable 
{
    int MAX_ALTITUDE = 10000; // public static final by default
    void fly();              // all methods are public abstract by default
}

// Abstract class = blueprint
abstract class Animal 
{
    String name; 

    Animal(String name) 
    {
        this.name = name;
    }

    abstract void makeSound();

    void eat() 
    {
        System.out.println(name + " is eating.");
    }
}

// Dog inherits Animal and also implements Flyable
class Dog extends Animal implements Flyable 
{
    Dog(String name) 
    {
        super(name);
    }

    @Override
    void makeSound() 
    {
        System.out.println("Woof!");
    }

    @Override
    public void fly() 
    {
        System.out.println("Dogs can't really fly, but imagine wings!");
    }
}

public class Demo 
{
    public static void main(String[] args) 
    {
        Dog d = new Dog("Buddy");
        d.makeSound();  // from Animal
        d.eat();        // concrete method from Animal
        d.fly();        // from Flyable
    }
}
```

---

## 🎯 Quick Rule of Thumb

* Use an **interface** for a **capability** shared across many unrelated classes.
* Use an **abstract class** for a **base class** with fields + methods for related subclasses.
* **Interfaces define the “what”**, while **abstract classes define the “what + how”**.

---

## 🎯 Learning Outcomes

* Define and use **interfaces** with `implements`.
* Understand **multiple inheritance** via interfaces.
* Use **default** and **static** methods in interfaces.
* Decide between **interface** vs **abstract class** for clean, flexible design.

---

