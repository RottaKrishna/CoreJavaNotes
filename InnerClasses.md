1)


## 🧠 What is an Inner Class?

An **Inner Class** is a class defined **within another class**.
It is also known as a **Nested Class**.

---

## 🎯 Why Use Inner Classes?

* To **logically group** classes that are only used in one place.
* To **reduce the complexity** of large classes.
* Inner class can access **private members** of outer class directly.
* Makes the code **more readable and encapsulated**.

---

## 🧩 Types of Inner Classes

| Type                    | Description                                       |
| ----------------------- | ------------------------------------------------- |
| **Member Class**        | Defined inside a class, **not static**.           |
| **Static Nested Class** | Defined with `static` keyword.                    |
| **Local Class**         | Defined **inside a method**.                      |
| **Anonymous Class**     | Defined without a name, used for **short usage**. |

---

## 💡 Example: **Member Inner Class**

### 🔷 Outer Class with Inner Class

```java
class Outer {
    int x = 10;

    void outerDisplay() {
        Inner i = new Inner();
        i.innerDisplay();
        System.out.println("Inner y = " + i.y);  // Accessing inner class member via object
    }

    class Inner {
        int y = 20;

        void innerDisplay() {
            System.out.println("Outer x = " + x);  // Access outer class member directly
            System.out.println("Inner y = " + y);
        }
    }
}
```

---

### 🔶 Usage (from another class)

```java
public class Test {
    public static void main(String[] args) {
        Outer outer = new Outer();
        outer.outerDisplay();

        // Accessing inner class directly from outside (not recommended)
        Outer.Inner inner = outer.new Inner();
        inner.innerDisplay();
    }
}
```

---

## 🔑 Key Points

| Concept                                   | Behavior                                          |
| ----------------------------------------- | ------------------------------------------------- |
| Inner class can access outer class fields | ✅ Allowed directly (like `x`)                     |
| Outer class accessing inner class fields  | ❌ Not directly allowed — needs inner class object |
| Object creation syntax (from outside)     | `Outer.Inner obj = outerObj.new Inner();`         |
| Compiled class file                       | `Outer$Inner.class`                               |

---

## 📌 Diagram (Text-Based)

```
+---------------------+
|     Outer Class     |
|  int x = 10         |
|  void outerDisplay()|----> creates Inner class object
|                     |
|  +----------------+ |
|  |  Inner Class   | |
|  |  int y = 20    |<---- can access x directly
|  |  void display()| |
|  +----------------+ |
+---------------------+
```

---

## ⚙️ Compilation Behavior

After compiling the `Outer.java` file:

```
Outer.class
Outer$Inner.class  <-- For inner class
```

---

## 📌 Summary Table

| Inner Class Feature           | Allowed? | Notes                                     |
| ----------------------------- | -------- | ----------------------------------------- |
| Access outer class variables  | ✅        | Directly                                  |
| Access inner class from outer | ✅        | Using object                              |
| Access inner from outside     | ✅        | Needs `Outer.Inner` + `outer.new Inner()` |
| Separate `.class` file        | ✅        | Generated as `Outer$Inner.class`          |

---

2)


## 🔁 Recap: What is a Nested Inner Class?

A **Nested Inner Class** is a class defined **within another class (non-static)**.

* Inner class has access to **all members of the outer class**, including private.
* Outer class **cannot directly** access members of inner class — needs an **object of inner class**.

---

## ✅ Full Working Code Based on Video

```java
// Outer.java
class Outer {
    int x = 10;

    // Member inner class
    class Inner {
        int y = 20;

        void innerDisplay() {
            System.out.println("Outer x = " + x);  // Access outer class variable
            System.out.println("Inner y = " + y);  // Own variable
        }
    }

    // Creating object of Inner inside Outer
    Inner i = new Inner(); // Object declared at class level

    void outerDisplay() {
        i.innerDisplay(); // Using inner object
        System.out.println("Access inner.y via object: " + i.y);
        // System.out.println(y); // ❌ Error: y is not a member of Outer
    }
}
```

```java
// NestedInner.java (Main class)
public class NestedInner {
    public static void main(String[] args) {
        // Step 1: Create Outer object
        Outer o = new Outer();

        // Step 2: Call outer method that uses Inner class
        o.outerDisplay();

        // --- Directly creating Inner object outside Outer class ---

        Outer.Inner oi = o.new Inner(); // OuterObject.new Inner()
        oi.innerDisplay(); // Can call method of inner class
    }
}
```

---

## ⚙️ Key Learnings from the Video

| Concept                                       | Code Example                                       | Output / Result                      |
| --------------------------------------------- | -------------------------------------------------- | ------------------------------------ |
| Access inner class inside outer class         | `Inner i = new Inner();`                           | ✅ Allowed                            |
| Inner class accesses outer class variable `x` | `System.out.println(x);`                           | ✅ Prints outer class variable        |
| Outer accesses inner variable `y` directly    | `System.out.println(y);`                           | ❌ Compile error                      |
| Outer accesses inner variable via object      | `System.out.println(i.y);`                         | ✅ Works                              |
| Inner class object declared inside method     | `Inner i = new Inner();` inside `outerDisplay()`   | Scope is method-level                |
| Inner class object declared at class level    | `Inner i = new Inner();` above method              | Usable by all methods in outer class |
| Directly accessing inner from main method     | `Outer.Inner oi = o.new Inner();`                  | ✅ Works, need Outer object first     |
| Static members in Outer                       | Can be accessed from Inner using class name        | ✅ Works                              |
| Class file names                              | Outer.class, NestedInner.class, Outer\$Inner.class | Java creates separate `.class` files |

---

## 🧪 Output Example

```
Outer x = 10
Inner y = 20
Access inner.y via object: 20
Outer x = 10
Inner y = 20
```

---

## 📁 Java Class Files Generated

After compiling the above code:

* `NestedInner.class` – main class
* `Outer.class` – outer class
* `Outer$Inner.class` – inner class

Java uses **`$`** in the filename to indicate that the class is **nested** inside another class.

---

## 🔚 Summary

* Inner classes help modularize and simplify large classes.
* They can **access outer members** directly.
* But outer class needs an **object** to access inner class members.
* You can create inner class objects both:

  * inside the outer class
  * or outside using: `Outer.Inner inner = outerObj.new Inner();`
* Inner classes compile into their own `.class` files using the format `Outer$Inner.class`.

---

3)


## 🔹 1. Local Inner Class (Defined Inside a Method)

### 💡 Concept:

* A **local inner class** is defined **inside a method**.
* It is **only accessible** within the method it is declared in.
* Useful for **limited scope**, like helper logic, or temporary overrides.

---

### ✅ Example Code:

```java
class Outer {
    void display() {
        // Local inner class defined inside method
        class Inner {
            void innerDisplay() {
                System.out.println("Hello from Local Inner Class!");
            }
        }

        Inner i = new Inner(); // Creating object of local inner class
        i.innerDisplay();      // Calling method
    }
}

public class LocalInnerDemo {
    public static void main(String[] args) {
        Outer o = new Outer();
        o.display();
    }
}
```

---

### 🔎 Output:

```
Hello from Local Inner Class!
```

---

### 📌 Notes:

| Feature                      | Explanation                                       |
| ---------------------------- | ------------------------------------------------- |
| Scope of inner class         | Only inside the method                            |
| Access to method variables   | Yes, but **only final or effectively final** vars |
| Can extend/implement classes | ✅ Yes, useful when implementing interface locally |
| Object creation              | After class declaration in same method            |

---

## 🔸 2. Anonymous Inner Class (Nameless Class Created on the Spot)

### 💡 Concept:

* A class **without a name**, created and defined **at the same time**.
* Used to **override abstract methods or implement interfaces quickly**.
* Saves boilerplate code when usage is **one-time only**.

---

### ✅ Example 1: Abstract Class

```java
abstract class My {
    abstract void display();
}

class Outer {
    void show() {
        My m = new My() { // Anonymous class
            void display() {
                System.out.println("Hello from Anonymous Class (Abstract)!");
            }
        };
        m.display();
    }
}

public class AnonymousAbstractDemo {
    public static void main(String[] args) {
        Outer o = new Outer();
        o.show();
    }
}
```

---

### ✅ Example 2: Interface

```java
interface My {
    void display();
}

class Outer {
    void show() {
        My m = new My() { // Anonymous class implementing interface
            public void display() {
                System.out.println("Hello from Anonymous Class (Interface)!");
            }
        };
        m.display();
    }
}

public class AnonymousInterfaceDemo {
    public static void main(String[] args) {
        Outer o = new Outer();
        o.show();
    }
}
```

---

### 🔎 Output (for both):

```
Hello from Anonymous Class (Abstract)!
Hello from Anonymous Class (Interface)!
```

---

### 📌 Notes:

| Feature    | Explanation                                                          |
| ---------- | -------------------------------------------------------------------- |
| Class name | No name given (anonymous)                                            |
| When used  | At the time of object creation                                       |
| Use case   | Implementing abstract class/interface without writing separate class |
| Common in  | Event handling, callbacks, built-in interface implementations        |

---

## 🔚 Final Takeaway

| Type              | Scope                 | Use Case                         | Object Creation Syntax                  |
| ----------------- | --------------------- | -------------------------------- | --------------------------------------- |
| Local Inner Class | Inside a method       | Helper classes inside method     | Declare class, then create object       |
| Anonymous Class   | Defined & used inline | Quick override or interface impl | `new Interface() { // implementation }` |

---

4)


## 🔹 Static Inner Class in Java

### 💡 Concept:

* A **static inner class** is like a regular class **declared inside another class** using the `static` keyword.
* It is **not tied to an instance** of the outer class.
* You **don’t need an object** of the outer class to use it.

---

### ✅ Syntax Overview:

```java
class Outer {
    static class Inner {
        void display() {
            System.out.println("Hello from Static Inner Class!");
        }
    }
}
```

---

### ✅ Full Example Code:

```java
class Outer {
    static int x = 10;
    int y = 20; // Non-static member

    // Static Inner Class
    static class Inner {
        void display() {
            System.out.println("Static variable x: " + x); // ✅ Allowed
            // System.out.println("Non-static variable y: " + y); ❌ Not Allowed
        }
    }
}

public class StaticInnerDemo {
    public static void main(String[] args) {
        // Creating object of static inner class without outer class object
        Outer.Inner obj = new Outer.Inner();
        obj.display();
    }
}
```

---

### 🔎 Output:

```
Static variable x: 10
```

---

### 📌 Key Points:

| Feature                       | Explanation                                                   |
| ----------------------------- | ------------------------------------------------------------- |
| Declared using                | `static class Inner {}`                                       |
| Access to outer class members | **Only static members** (cannot access `non-static` like `y`) |
| Object creation syntax        | `Outer.Inner obj = new Outer.Inner();`                        |
| Outer class object needed?    | ❌ No                                                          |
| Useful when                   | Inner class logic doesn't depend on outer class instance      |

---

### 🔄 Comparison with Regular Inner Class:

| Aspect               | Regular Inner Class               | Static Inner Class                    |
| -------------------- | --------------------------------- | ------------------------------------- |
| Access to outer vars | Both static and non-static ✅      | Only static variables ✅               |
| Needs outer object?  | ✅ Yes                             | ❌ No                                  |
| Object creation      | `new Outer().new Inner()`         | `new Outer.Inner()`                   |
| Common use           | When inner class depends on outer | When it's independent of outer object |

---

### 📘 Bonus: Use Case of Static Inner Class

Used when:

* The inner class is a **utility/helper** that doesn’t rely on outer class object.
* Example: Builders in design patterns, enums, constants grouping.

---

5)


## 🎯 Goal: Learn **Local Inner Classes**, **Anonymous Inner Classes**, and **Static Inner Classes** through practical demo.

---

## 🔹 1. Local Inner Class

### ✅ Definition:

A **Local Inner Class** is defined **inside a method**, and its **scope is limited** to that method only.

### ✅ Code:

```java
class Outer {
    public void display() {
        class Inner {
            void show() {
                System.out.println("Hello");
            }
        }
        Inner i = new Inner(); // Object creation
        i.show();              // Calling method
    }
}

public class Demo {
    public static void main(String[] args) {
        Outer o = new Outer();
        o.display(); // Output: Hello
    }
}
```

### ✅ Anonymous Object Version:

```java
class Outer {
    public void display() {
        class Inner {
            void show() {
                System.out.println("Hello");
            }
        }
        new Inner().show(); // Anonymous object
    }
}
```

---

## 🔹 2. Anonymous Inner Class

### ✅ Definition:

An **Anonymous Inner Class** is used to **extend abstract classes or implement interfaces** instantly, **without giving the class a name**.

---

### ✅ Case 1: Using Abstract Class

```java
abstract class My {
    abstract void show();
}

class Outer {
    public void display() {
        My m = new My() {
            void show() {
                System.out.println("Hello from Anonymous Inner Class");
            }
        };
        m.show();
    }
}
```

### ✅ Without Reference (Anonymous Object + Anonymous Class)

```java
class Outer {
    public void display() {
        new My() {
            void show() {
                System.out.println("Hello from Anonymous Class");
            }
        }.show();
    }
}
```

---

### ✅ Case 2: Using Interface

```java
interface My {
    void show();
}

class Outer {
    public void display() {
        My m = new My() {
            public void show() {
                System.out.println("Hello from Interface");
            }
        };
        m.show();
    }
}
```

---

## 🔹 3. Static Inner Class

### ✅ Definition:

* A **static inner class** is a static member of the outer class.
* It can access **only static members** of the outer class.
* Can be created **without creating outer class object**.

### ✅ Code:

```java
class Outer {
    static int y = 20; // Static variable
    int x = 10;        // Non-static (cannot be accessed by static inner class)

    static class My {
        void show() {
            System.out.println("Static y = " + y); // ✅
            // System.out.println("x = " + x); ❌ Not allowed
        }
    }
}

public class Demo {
    public static void main(String[] args) {
        Outer.My m = new Outer.My(); // No need of Outer object
        m.show(); // Output: Static y = 20
    }
}
```

---

## 📌 Summary Table

| Inner Class Type      | Defined In    | Needs Outer Class Object | Can Access Outer Members      | Common Use                             |
| --------------------- | ------------- | ------------------------ | ----------------------------- | -------------------------------------- |
| Local Inner Class     | Inside method | ✅ Yes                    | Yes (including private)       | Logic restricted to a method           |
| Anonymous Inner Class | Inside method | ✅ Yes                    | Only final/static effectively | One-time use (usually with interface)  |
| Static Inner Class    | Inside class  | ❌ No                     | Only static members           | Helper class (like utility or builder) |

---








