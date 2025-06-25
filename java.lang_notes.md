1)


---

## 📦 `java.lang` Package — The Default Package

* **Auto-imported** in every Java program.
* No need to explicitly import it:
  `import java.lang.*;` is done by default.

---

## 👑 `Object` Class — *The Mother of All Java Classes*

| Feature          | Description                                         |
| ---------------- | --------------------------------------------------- |
| 📌 Location      | `java.lang.Object`                                  |
| 🌐 Superclass of | All Java classes (including user-defined ones)      |
| 🔄 Inheritance   | Every class directly or indirectly extends `Object` |

---

## 🔧 Common Methods in `Object` Class

| Method                                | Purpose                                                                                        |
| ------------------------------------- | ---------------------------------------------------------------------------------------------- |
| `clone()`                             | Creates and returns a copy (clone) of the object. *(Protected)*                                |
| `equals(Object o)`                    | Compares if two object references point to the same object.                                    |
| `finalize()`                          | Called by Garbage Collector before object is removed from memory. Like C++ destructor.         |
| `getClass()`                          | Returns runtime class of object.                                                               |
| `hashCode()`                          | Returns a hash code (unique ID) for the object.                                                |
| `notify()` / `notifyAll()` / `wait()` | Used for thread communication (Multithreading).                                                |
| `toString()`                          | Returns string representation of the object. Called automatically in `System.out.println(obj)` |

---

## 🧪 Code Experiments & Notes

### ✅ Example: Default Methods

```java
public class Main {
    public static void main(String[] args) {
        Object o1 = new Object();
        System.out.println(o1.toString()); // java.lang.Object@hashcode
        System.out.println(o1.hashCode()); // some unique int
    }
}
```

### ✅ `.equals()` Behavior

```java
Object o1 = new Object();
Object o2 = new Object();
System.out.println(o1.equals(o2)); // false

Object o3 = o1;
System.out.println(o1.equals(o3)); // true
```

### ✅ `.toString()` Behavior

```java
System.out.println(o1);          // Calls o1.toString() automatically
System.out.println(o1.toString()); // Same result
```

---

## 🛠️ Custom Class Inheriting `Object`

Even if you don’t extend explicitly, it's still inherited:

```java
class MyObject {}

class MyObject2 extends MyObject {}

public class Main {
    public static void main(String[] args) {
        MyObject2 o2 = new MyObject2();
        System.out.println(o2.toString());  // Inherited from Object
    }
}
```

---

## 🔄 Method Overriding from `Object` Class

### ✅ Overriding `toString()`

```java
class MyObject {
    public String toString() {
        return "MyObject";
    }
}
```

### ✅ Overriding `hashCode()` and `equals()`

```java
class MyObject {
    public int hashCode() {
        return 100; // Not unique, just for demo
    }

    public boolean equals(Object o) {
        return this.hashCode() == o.hashCode(); // BAD PRACTICE: For learning only
    }
}
```

### ❌ Cannot Override Final Methods

```java
// Error: Cannot override final method
// public void wait() {} ❌
```

---

## 🎯 Best Practices

| Method            | Override?    | Notes                                                               |
| ----------------- | ------------ | ------------------------------------------------------------------- |
| `toString()`      | ✅ Yes        | For better logging/debugging                                        |
| `equals()`        | ✅ If Needed  | When comparing object contents                                      |
| `hashCode()`      | ❌ Usually No | Only override if needed (must maintain consistency with `equals()`) |
| `wait()/notify()` | ❌ No         | Final methods — cannot override                                     |

---

## 🧠 Summary Key Points

* `Object` is the universal superclass.
* All classes (even your own) inherit from it.
* Common methods: `equals()`, `hashCode()`, `toString()`, and threading-related methods.
* `toString()` is automatically called when printing objects.
* Override methods wisely (especially equals/hashCode together).
* Thread-related methods are already built-in, showing Java supports multithreading at its core.

---

2)


## 🎁 What are Wrapper Classes?

> Java has **primitive data types** like `int`, `float`, `char`, `boolean`, etc., which are **not objects**.

But Java is an **object-oriented** language, and to treat everything as objects, **wrapper classes** are used.

🧊 **Wrapper Class = A Class that "wraps" a primitive into an object**

---

### ✅ Example:

```java
int i = 10; // primitive
Integer obj = Integer.valueOf(i); // wrapper object
```

---

## 📦 List of Wrapper Classes in Java

| Primitive | Wrapper Class |
| --------- | ------------- |
| `byte`    | `Byte`        |
| `short`   | `Short`       |
| `int`     | `Integer`     |
| `long`    | `Long`        |
| `float`   | `Float`       |
| `double`  | `Double`      |
| `char`    | `Character`   |
| `boolean` | `Boolean`     |

All are present in `java.lang` package — no need to import manually.

---

## 🧬 Class Hierarchy

```
        Object
       /  |   \
 Number  Boolean  Character
   |
   ├── Byte
   ├── Short
   ├── Integer
   ├── Long
   ├── Float
   └── Double
```

All numeric wrappers inherit from `Number` class.
`Character` and `Boolean` do **not**, but all inherit from `Object`.

---

## 🛠️ Common Methods in Wrapper Classes

These methods help **convert between types**:

```java
byteValue()
intValue()
floatValue()
doubleValue()
shortValue()
longValue()
```

All defined in `Number` class (abstract) and overridden in each wrapper.

---

## 🔨 Ways to Create Wrapper Objects

### ✅ Recommended Method (Factory method):

```java
Integer a = Integer.valueOf(10);  // Good
```

### ❌ Deprecated (Constructor):

```java
Integer a = new Integer(10);  // Not recommended
```

### ✅ Direct assignment (Auto Boxing):

```java
Integer b = 10;  // Internally calls valueOf()
```

---

## 🔁 Boxing & Unboxing (Important Concept)

### 📦 Boxing

Converting primitive → object

```java
int a = 10;
Integer b = Integer.valueOf(a);  // Manual Boxing
Integer b = a;                   // Auto Boxing
```

### 🔓 Unboxing

Converting object → primitive

```java
Integer b = 10;
int a = b.intValue(); // Manual Unboxing
int a = b;            // Auto Unboxing
```

---

## 🧃 Real Examples:

### ✅ Float Example with `valueOf()` and `floatValue()`

```java
Float h = Float.valueOf("123.5"); // wrapper from string
float x = h.floatValue();         // manual unboxing
float y = h;                      // auto unboxing
```

---

## 📦 Boxing & Unboxing Diagram

```
Primitive      ->       Wrapper Object
  (int a=10)             (Integer b=a)      => Boxing

Wrapper Object ->       Primitive
  (Integer b=10)         (int a=b)          => Unboxing
```

---

## 🔥 Summary Table

| Concept       | Description                   | Code Example                        |
| ------------- | ----------------------------- | ----------------------------------- |
| Boxing        | primitive → object            | `Integer obj = Integer.valueOf(5);` |
| Auto Boxing   | automatic conversion          | `Integer obj = 5;`                  |
| Unboxing      | object → primitive            | `int x = obj.intValue();`           |
| Auto Unboxing | automatic object to primitive | `int x = obj;`                      |

---

## 💡 Key Notes

* Wrapper classes allow primitives to be used in **collections**, **generics**, and **object-required** places.
* **Auto Boxing** and **Auto Unboxing** introduced in **Java 5+**
* Avoid constructors like `new Integer(5)` — they are deprecated.
* You can pass both **string** and **primitive** to `valueOf()`.

---

## 🧠 Final Tip

> ✨ "Explore the wrapper classes by practicing — convert between types, pass values, and see how auto-boxing & unboxing make your code clean." ✨

---

3)


Java’s `Integer` class is a **wrapper** around the primitive type `int`. It provides many utility methods that help with conversions, comparisons, and working with different number systems.

---

### 📌 1. **Creating Integer Objects**

```java
int m1 = 15;
Integer m2 = m1;  // Auto-boxing
```

### 📌 2. **Methods from `Number` Class**

These methods are inherited from the `Number` class:

```java
m2.byteValue()
m2.floatValue()
m2.intValue()
m2.longValue()
```

---

### 📌 3. **Comparison Methods**

#### 🔸 `compareTo(Integer other)`

* Returns `0` if equal, `>0` if greater, `<0` if smaller.

```java
Integer m2 = 15;
Integer m3 = 20;
System.out.println(m2.compareTo(m3)); // Output: -1
```

#### 🔸 `equals(Object obj)`

* Compares the **values**, not the references.

```java
System.out.println(m2.equals(m1));  // true (primitive allowed)
System.out.println(m2.equals(m3));  // true (if same value)
```

---

### 📌 4. **Static Factory Method: `valueOf()`**

```java
Integer i1 = Integer.valueOf("123");             // from string
Integer i2 = Integer.valueOf(123);               // from int
Integer i3 = Integer.valueOf("1010", 2);         // binary to decimal
Integer i4 = Integer.valueOf("A7", 16);          // hex to decimal
```

---

### 📌 5. **`parseInt()` Method**

Converts `String` to `int`.

```java
int num = Integer.parseInt("123");
System.out.println(num); // 123
```

🔻 Throws `NumberFormatException` if input is not valid.

```java
Integer.parseInt("123a"); // Error
```

---

### 📌 6. **`decode()` Method**

Parses a string into an `Integer`, recognizing **prefixes**:

* `0x` or `0X` → Hex
* `0` → Octal
* No prefix → Decimal

```java
Integer i = Integer.decode("0xA7"); // 167
```

---

### 📌 7. **Useful Static Fields & Methods**

#### 🧾 Constants

```java
Integer.MAX_VALUE
Integer.MIN_VALUE
Integer.BYTES      // Size in bytes (4)
```

#### 🧠 `bitCount(int)`

Counts number of 1s in the binary representation.

```java
System.out.println(Integer.bitCount(7)); // 3 → 111
```

#### 🔄 `reverseBytes(int)`

Reverses byte order of an integer.

```java
int result = Integer.reverseBytes(128);
// Can be equal to Integer.MIN_VALUE
System.out.println(result == Integer.MIN_VALUE); // true
```

#### 🔃 Bit Rotations

```java
Integer.rotateLeft(num, n);
Integer.rotateRight(num, n);
```

#### ➕ `sum(int a, int b)`

```java
Integer.sum(10, 20); // 30
```

#### ➕ `signum(int)`

Returns `-1`, `0`, or `1` depending on sign.

```java
Integer.signum(-10); // -1
```

#### 🔢 `toBinaryString(int)`

Converts to binary string.

```java
System.out.println(Integer.toBinaryString(40)); // 101000
```

Similarly, other conversion methods:

* `toHexString()`
* `toOctalString()`

---

### 📌 Summary Table of Key Methods

| Method / Field               | Description                    |
| ---------------------------- | ------------------------------ |
| `valueOf()`                  | Converts string/int to Integer |
| `parseInt()`                 | Converts string to int         |
| `equals()`                   | Compares values                |
| `compareTo()`                | Compares Integer objects       |
| `decode()`                   | Parses string with radix hints |
| `bitCount()`                 | Number of 1-bits in binary     |
| `reverseBytes()`             | Reverses byte order            |
| `rotateLeft()/rotateRight()` | Binary rotations               |
| `signum()`                   | Sign of a number               |
| `toBinaryString()`           | Decimal to binary string       |
| `MAX_VALUE / MIN_VALUE`      | Constant fields                |

---

**📚 Final Note:**
Most used methods in real-world:

* `parseInt()`
* `valueOf()`
* `equals()`
* `compareTo()`

Other methods like `reverseBytes()` are advanced and used in systems-level programming.

---

4)


Here's a **structured and simplified summary** of the video content on `Float`, `Character`, and `Boolean` wrapper classes in Java, along with **key methods** and **code examples**.

---

### 🟩 **Float Class**

Float is a wrapper class for the `float` primitive and it **extends the `Number` class**, so it shares some methods with `Integer`.

#### ✅ Basic Example:

```java
float a = 12.5f;
Float b = 12.5f;

System.out.println(b.equals(a)); // true
```

* Compares values, not object references.

---

### ✅ **Useful Methods in `Float`**

#### 1. `isInfinite()`

Checks if the number is **infinite**.

```java
Float b = 12.5f / 0; // Results in Infinity
System.out.println(b.isInfinite()); // true
```

#### 2. Comparing with Constants:

```java
System.out.println(b.equals(Float.POSITIVE_INFINITY)); // true
```

```java
Float b = -12.5f / 0;
System.out.println(b.equals(Float.NEGATIVE_INFINITY)); // true
```

---

#### 3. `isNaN()` – Not a Number

Use this to check if the value is **NaN (Not a Number)**.

```java
Float b = (float)Math.sqrt(-1); // results in NaN
System.out.println(b.isNaN()); // true
```

> ⚠️ Do **not** use `.equals(Float.NaN)` for comparison. It will always return false.

```java
System.out.println(Float.NaN == Float.NaN); // false
System.out.println(Float.NaN != Float.NaN); // true
```

---

### 🟨 **Character Class**

Unlike `Float`, this class **does not inherit from `Number`**. It works with `char` values and provides many **utility static methods**.

#### ✅ Example:

```java
Character c = 'A';
System.out.println(Character.toLowerCase(c)); // a
System.out.println(Character.isLetter(c)); // true
System.out.println(Character.isDigit(c)); // false
System.out.println(Character.isUpperCase(c)); // true
```

#### 📌 Methods:

* `isLetter()`, `isDigit()`, `isUpperCase()`, `isLowerCase()`
* `toUpperCase()`, `toLowerCase()`
* `isWhitespace()`, `isLetterOrDigit()`

---

### 🟦 **Boolean Class**

Wrapper for `boolean` primitive. Useful for logical operations and parsing.

#### ✅ Example:

```java
Boolean b = true;
System.out.println(Boolean.parseBoolean("true")); // true

System.out.println(Boolean.logicalAnd(true, false)); // false
System.out.println(Boolean.logicalOr(true, false));  // true
System.out.println(Boolean.logicalXor(true, false)); // true
```

---

### 📝 Summary Table

| Class     | Key Methods / Constants                                             | Description                          |
| --------- | ------------------------------------------------------------------- | ------------------------------------ |
| Float     | `isInfinite()`, `isNaN()`, `POSITIVE_INFINITY`, `NEGATIVE_INFINITY` | Check for special float values       |
| Character | `isLetter()`, `isDigit()`, `toUpperCase()`, `toLowerCase()`         | Validate or convert character values |
| Boolean   | `parseBoolean()`, `logicalAnd()`, `logicalOr()`, `logicalXor()`     | Operate on or parse boolean values   |

---

✨ **Tips:**

* Use `.isNaN()` for float/double, not `== Float.NaN`
* Use `Character` methods instead of manually checking ASCII
* Wrapper classes are powerful when working with **collections**, **nullability**, or **utility operations**


5)


### ✅ **Core Concepts Recap**

#### 1. **String Class**

* A **sequence of characters** (e.g., `"hello"`).
* **Immutable**: Once created, it **cannot be modified**.
* When changes like concatenation occur, a **new object is created**.
* Common methods:

  * `charAt()`, `concat()`, `contains()`, `equals()`, `indexOf()`, `lastIndexOf()`

##### 🔸 Example:

```java
String s = "hello";
s.concat(" world"); // creates a new object
System.out.println(s); // prints "hello"
```

---

#### 2. **StringBuffer Class**

* Like `String`, but **mutable**.
* **Thread-safe**: Uses **synchronized** methods to prevent multiple threads from modifying at the same time.
* Default capacity: **16 characters**, can grow dynamically.
* Methods:

  * `append()`, `insert()`, `deleteCharAt()`, `reverse()`, `substring()`

##### 🔸 Example:

```java
StringBuffer sb = new StringBuffer("hello");
sb.append(" world");
System.out.println(sb); // prints "hello world"
```

---

#### 3. **StringBuilder Class**

* Same as `StringBuffer` (also **mutable**), but:
* **Not thread-safe** (no synchronization).
* Hence, **faster** than `StringBuffer` in single-threaded environments.
* Methods are exactly the same as `StringBuffer`.

##### 🔸 Example:

```java
StringBuilder sb = new StringBuilder("hello");
sb.append(" world");
System.out.println(sb); // prints "hello world"
```

---

### 🔁 **Comparison Table**

| Feature              | `String`                    | `StringBuffer`                                | `StringBuilder`                                     |
| -------------------- | --------------------------- | --------------------------------------------- | --------------------------------------------------- |
| Mutability           | ❌ Immutable                 | ✅ Mutable                                     | ✅ Mutable                                           |
| Thread-safe          | ✅ (Immutable)               | ✅ Yes (Synchronized)                          | ❌ No                                                |
| Performance          | Fast (immutable)            | Slower (thread safety adds overhead)          | Faster (no synchronization)                         |
| Common Methods       | `concat()`, `charAt()` etc. | `append()`, `insert()`, `reverse()`           | Same as `StringBuffer`                              |
| Usage Recommendation | Use when data never changes | Use when multiple threads access mutable data | Use in single-threaded or performance-critical code |

---

### 🧠 Notes on Capacity

* Default capacity of `StringBuffer` / `StringBuilder` is **16**.
* When exceeded, capacity is **automatically increased**.
* `length()` shows current string length, `capacity()` shows total buffer capacity.

---

### 🧪 Output Program Recap

```java
String s1 = "hello";
StringBuffer s2 = new StringBuffer("hello");
StringBuilder s3 = new StringBuilder("hello");

s1.concat(" world"); // doesn't modify s1
s2.append(" world"); // modifies s2
s3.append(" world"); // modifies s3

System.out.println(s1); // hello
System.out.println(s2); // hello world
System.out.println(s3); // hello world
```

🟢 **Output:**

```
hello
hello world
hello world
```

---

### 🧵 Thread Safety Insight

* `StringBuffer` prevents **multiple threads** from calling methods like `append()` simultaneously using **synchronized** blocks.
* In contrast, `StringBuilder` does **not** prevent simultaneous access—faster but **unsafe in multithreaded scenarios**.

---

### 🔚 Conclusion

* Use **`String`** when immutability is preferred.
* Use **`StringBuilder`** when working in **single-threaded** environments and need mutability.
* Use **`StringBuffer`** when working in **multithreaded** environments needing thread safety.

---

6)


## 🌟 What is `Enum` in Java?

* `enum` stands for **enumerated data type**.
* Like **classes** define user-defined types, **enums** define a **fixed set of constants**.
* Used for **readable and maintainable code** where predefined constant values are needed.

---

## 📌 Syntax of Enum

```java
enum DEPT {
    CS, IT, CIVIL, ECE;
}
```

* Each item (`CS`, `IT`, etc.) is:

  * `public`
  * `static`
  * `final`
* You **don’t assign values**, the name **itself is the value**.

---

## ✅ Enum Usage Example

```java
DEPT d = DEPT.CS;
System.out.println(d);  // Output: CS
```

* You can only assign a value defined in the `enum`.
* `DEPT d = 1;` → ❌ Compilation error.

---

## 🔄 Enum in Switch Case

```java
switch (d) {
    case CS:
        System.out.println("Head: John, Block A");
        break;
    case IT:
        System.out.println("Head: Ravi, Block B");
        break;
    // and so on...
}
```

---

## 🔍 Useful Enum Methods (inherited from `java.lang.Enum`)

| Method       | Description                              | Example                 |
| ------------ | ---------------------------------------- | ----------------------- |
| `.name()`    | Returns name of the enum constant        | `DEPT.CS.name()` → "CS" |
| `.ordinal()` | Returns index of enum constant (0-based) | `DEPT.IT.ordinal()` → 1 |
| `.valueOf()` | Convert string to enum constant          | `DEPT.valueOf("ECE")`   |
| `.values()`  | Returns array of all constants           | `DEPT.values()`         |

---

## 🔁 Iterate Over Enum Values

```java
for (DEPT dept : DEPT.values()) {
    System.out.println(dept);
}
// Output: CS IT CIVIL ECE
```

---

## 🛠️ Enum Constructor and Methods

You can define:

* **Constructor** (only `private` or package-default)
* **Methods** (public is allowed)
* **Fields (properties)**

### Example: Adding data to enum constants

```java
enum DEPT {
    CS("John", "A"),
    IT("Ravi", "B"),
    CIVIL("Srinivas", "C"),
    ECE("Dave", "D");

    private final String head;
    private final String location;

    // Constructor
    DEPT(String head, String location) {
        this.head = head;
        this.location = location;
    }

    // Getter methods
    public String getHeadName() {
        return head;
    }

    public String getLocation() {
        return location;
    }
}
```

### Usage:

```java
DEPT d = DEPT.CS;
System.out.println(d.getHeadName());   // Output: John
System.out.println(d.getLocation());   // Output: A
```

---

## 🔄 When is the Enum Constructor Called?

* **Once for each constant** during class loading.
* Even if you assign only one, all enum constants are **created at once**.

---

## ✅ Summary Checklist

| Feature                          | Supported in Enum? |
| -------------------------------- | ------------------ |
| Defining constants               | ✅ Yes              |
| Constructors                     | ✅ Yes (private)    |
| Methods                          | ✅ Yes              |
| Fields                           | ✅ Yes              |
| Use in switch-case               | ✅ Yes              |
| Iterable using `.values()`       | ✅ Yes              |
| Accessing metadata (name, index) | ✅ Yes              |

---














