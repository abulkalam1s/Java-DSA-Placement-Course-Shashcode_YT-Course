# Java Packages?
A java package is a group of similar types of classes, interfaces and sub-packages.
Package in java can be categorized in two form, built-in package and user-defined package.
There are many built-in packages such as java, lang, awt, javax, swing, net, io, util, sql etc.
It provides access protection.
It removes naming collision.

There are three ways to access the package from outside the package:
1. import package.*; // classes and interfaces will be accessible but not subpackages.
2. import package.classname; //only declared class of this package will be accessible.
3. fully qualified name. //only declared class of this package will be accessible and there is no need to import

// java.util and java.sql packages contain Date class, so it is better to use fully qualified names.
// Note: Subpackages are needed to be imported explicitly, as they won't be part of parent package import.  

Sequence that needs to be followed:
1. first declare package
2. then import the package
3. then declare your class

System is available in java lang package.

In java, we use a specific format for defining the package names.
Standard-> domain.company.package
Example-> com.youtube.shashwat

Note: lang package is imported by default.

# Modifiers in Java
-----------------------------------
Modifiers in Java are keywords that modify the behavior of classes, methods, constructors, and variables. They are classified into two broad categories: **Access Modifiers** and **Non-Access Modifiers**.

---

### **1. Access Modifiers**
Access modifiers define the visibility or accessibility of classes, methods, constructors, and variables. 

#### **Types of Access Modifiers:**
| Modifier   | Class | Package | Subclass (other package) | Global |
|------------|-------|---------|--------------------------|--------|
| `public`   | ✅    | ✅      | ✅                       | ✅     |
| `protected`| ✅    | ✅      | ✅ (only via inheritance)| ❌     |
| `default`* | ✅    | ✅      | ❌                       | ❌     |
| `private`  | ✅    | ❌      | ❌                       | ❌     |

> *Default (no modifier): When no access modifier is specified, it is considered "default" (package-private).

#### **Details:**
- **`public`**:
  - Accessible everywhere.
  - Example:
    ```java
    public class MyClass {
        public void show() {
            System.out.println("Accessible everywhere");
        }
    }
    ```

- **`protected`**:
  - Accessible within the same package and subclasses in different packages.
  - Example:
    ```java
    public class Parent {
        protected void display() {
            System.out.println("Protected method");
        }
    }
    
    public class Child extends Parent {
        public void show() {
            display(); // Accessible here
        }
    }
    // more detailed explanation see below
    ```

- **`default`** (no modifier):
  - Accessible only within the same package.
  - Example:
    ```java
    class MyClass {
        void show() { // Default access
            System.out.println("Package-private access");
        }
    }
    ```

- **`private`**:
  - Accessible only within the same class.
  - Example:
    ```java
    public class MyClass {
        private void show() {
            System.out.println("Private method");
        }
    }
    ```

---

### **2. Non-Access Modifiers**
These modify the behavior and implementation of classes, methods, and variables.

#### **Types of Non-Access Modifiers:**

1. **`static`**:
   - Used to create fields or methods that belong to the class rather than any instance.
   - Example:
     ```java
     public class MyClass {
         static int count = 0; // Class-level variable
         static void show() {
             System.out.println("Static method");
         }
     }
     ```
 A. Static Block - 
 If you need to do the computation in order to initialize your static variables, you can declare a static block that gets executed exactly once, when the class is 
 first loaded. 

 int a=2;
 int b=0;

  // static block
    static {
        System.out.println("Static block initialized.");
        b = a * 7 + 2;
    }

  B. Static Variable - 
  When a variable is declared as static, then a single copy of the variable is created and shared among all objects at the class level.
  We can create static variables at the class level only
  static block and static variables are executed in the order they are present in a program.

  C. Static Method -
  When a method is declared with the static keyword, it is known as the static method. The most common example of a static method is the main() method.
  Methods declared as static have several restrictions: 
    1. They can only directly call other static methods.
    2. They can only directly access static data.
    3. They cannot refer to "this" or "super" in any way.

  D. Static Classes - 
  A class can be made static only if it is a nested class. We cannot declare a top-level class with a static modifier but can declare nested classes as static.      Such types of classes are called Nested static classes. Nested static class doesn’t need a reference of Outer class. In this case, a static class cannot access    non-static members of the Outer class.

2. **`final`**:
   - Prevents modification:
     - `final` class: Cannot be subclassed.
     - `final` method: Cannot be overridden.
     - `final` variable: Value cannot be changed.
   - Example:
     ```java
     final class MyFinalClass { }
     class MyClass {
         final int MAX_VALUE = 100;
         final void display() {
             System.out.println("Cannot override this method");
         }
     }
     ```

3. **`abstract`**:
   - Used with classes and methods:
     - `abstract` class: Cannot be instantiated.
     - `abstract` method: Must be implemented in subclasses.
   - Example:
     ```java
     abstract class Animal {
         abstract void sound();
     }

     class Dog extends Animal {
         void sound() {
             System.out.println("Barks");
         }
     }
     ```

4. **`synchronized`**:
   - Ensures thread-safe execution of methods or blocks.
   - Example:
     ```java
     public class MyClass {
         public synchronized void show() {
             System.out.println("Thread-safe method");
         }
     }
     ```

5. **`volatile`**:
   - Ensures visibility of changes to a variable across threads.
   - Example:
     ```java
     public class MyClass {
         private volatile boolean flag = true;
     }
     ```

6. **`transient`**:
   - Excludes fields from serialization.
   - Example:
     ```java
     public class MyClass implements Serializable {
         transient int id; // Not serialized
         String name;
     }
     ```

7. **`native`**:
   - Indicates a method is implemented in native code (e.g., C/C++).
   - Example:
     ```java
     public class MyClass {
         public native void display();
     }
     ```

8. **`strictfp`**:
   - Ensures consistent floating-point operations across platforms.
   - Example:
     ```java
     strictfp class MyClass {
         double calculate() {
             return 0.1 + 0.2;
         }
     }
     ```

---

### **Key Points to Remember**
- **Access Modifiers** control visibility and access levels.
- **Non-Access Modifiers** define specific behaviors, such as immutability, threading, or class-level scope.
- Combining modifiers is possible (e.g., `public static`, `private final`), but some combinations like `abstract final` are invalid.

Modifiers are essential for encapsulation, inheritance, and creating robust and secure Java applications.
_______________________________________________________________________________________________________________________
_______________________________________________________________________________________________________________________

**1 :- 
Here’s an example to demonstrate the **protected** access modifier in Java:

### Package: `mypackage`

#### Parent Class: `Animal.java`
`````````````````````````````````````````````````````````````````````````````````
package mypackage;

public class Animal {
    protected void display() {
        System.out.println("This is a protected method in the Animal class.");
    }
}
`````````````````````````````````````````````````````````````````````````````````

### Package: `anotherpackage`

#### Child Class: `Dog.java`
`````````````````````````````````````````````````````````````````````````````````
package anotherpackage;

import mypackage.Animal;

public class Dog extends Animal {
    public void show() {
        // Accessing the protected method of the parent class
        display();
    }
}
`````````````````````````````````````````````````````````````````````````````````
#### Non-Child Class: `Test.java`
`````````````````````````````````````````````````````````````````````````````````
package anotherpackage;

import mypackage.Animal;

public class Test {
    public static void main(String[] args) {
        Animal animal = new Animal();
        // animal.display(); // This will cause a compilation error because 'display' is protected

        Dog dog = new Dog();
        dog.show(); // Works because Dog is a subclass of Animal
    }
}
`````````````````````````````````````````````````````````````````````````````````
### Explanation:

1. **Within Package**:
   - In the `mypackage` package, any class (like a sibling class to `Animal`) can access the `protected` method `display()`.

2. **Outside the Package**:
   - A subclass (`Dog`) in the `anotherpackage` package can access the `protected` method through inheritance.
   - However, a non-subclass (`Test`) cannot directly access the `protected` method, even if it's in the same package as the subclass.

### Output:
When `Test` is run, it will print:
`````````````````````````````````````````````````````````````````````````````````
This is a protected method in the Animal class.
`````````````````````````````````````````````````````````````````````````````````

This demonstrates that **protected** members can be accessed in a child class outside the package, but not directly in a non-child class. 
