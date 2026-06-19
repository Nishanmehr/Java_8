### Why Java 8 Was Introduced?

Java 8 was introduced to make Java programming easier and more efficient.

- Reduce lengthy and repetitive code.
- Support Functional Programming using Lambda Expressions.
- Process collections easily using Stream API.
- Improve performance with Parallel Processing.
- Write cleaner, more readable, and maintainable code.

### Most Important Java 8 Features

- Lambda Expressions
- Functional Interfaces
- Stream API
- Method References
- Default Methods
- Optional Class
- Date and Time API
- Parallel Streams# Lambda Expression

# 1.LAMBDA EXPRESSION
A **Lambda Expression** is an **anonymous function**.

It does not have:
- Name
- Return Type
- Access Modifier

Lambda Expressions were introduced in **Java 8** to write code in a shorter and cleaner way.

### Syntax

```java
(parameters) -> expression
```

### Steps to Create a Lambda Expression

#### Before Lambda

```java
public int add(int a, int b) {
    return a + b;
}
```

#### Step 1: Remove Modifier

```java
int add(int a, int b) {
    return a + b;
}
```

#### Step 2: Remove Return Type

```java
add(int a, int b) {
    return a + b;
}
```

#### Step 3: Remove Method Name and Add Arrow

```java
(int a, int b) -> {
    return a + b;
}
```

#### Step 4: Type Inference (Remove Data Types)

```java
(a, b) -> {
    return a + b;
}
```

#### Step 5: Remove Return Keyword and Curly Braces (Single Statement)

```java
(a, b) -> a + b
```

#### Step 6: If Only One Parameter, Remove Parentheses

```java
x -> x * x
```

### Benefits of Lambda Expression

- Smaller and cleaner code
- Enables Functional Programming
- Works with Functional Interfaces
- Reduces jar file size
- Eliminates creation of extra anonymous classes
- Avoids shadow variable issues
- Improves code readability
#
## Interview Answer

**Lambda Expression is an anonymous function that has no name, no return type, and no access modifier. It is used to write shorter and cleaner code and is mainly used with Functional Interfaces.**

# 2.Functional Interface

A **Functional Interface** is an interface that contains **exactly one abstract method (SAM - Single Abstract Method)**.

It is mainly used to **invoke Lambda Expressions**.

### Declaration

```java
@FunctionalInterface
interface MyInterface {
    void display();
}
```

> `@FunctionalInterface` is optional but recommended. It ensures that the interface contains only one abstract method.

### Rules

- Must contain exactly **one abstract method**.
- Can contain multiple **default methods**.
- Can contain multiple **static methods**.
- Can contain methods inherited from `Object` class.

### Before Java 8

Until Java 7, interfaces could contain only:

```java
public abstract void show();
```

All methods were implicitly `public abstract`.

### Since Java 8

Interfaces can also contain:

### Default Methods

```java
interface MyInterface {
    default void sayHello() {
        System.out.println("Hello");
    }
}
```

### Static Methods

```java
interface MyInterface {
    static void greet() {
        System.out.println("Welcome");
    }
}
```

### Why Default Methods?

Default methods allow us to add new methods to an interface without breaking existing implementations.

Classes can use the default implementation directly without overriding it.

### Multiple Default Method Conflict

If two interfaces have the same default method, the implementing class must override it.

#### Example

```java
interface A {
    default void sayHello() {
        System.out.println("Hello");
    }
}

interface B {
    default void sayHello() {
        System.out.println("Say Hello");
    }
}

public class MyClass implements A, B {

    @Override
    public void sayHello() {
        B.super.sayHello();
    }

    public static void main(String[] args) {
        MyClass m = new MyClass();
        m.sayHello();
    }
}
```

#### Output

```text
Say Hello
```

### Benefits

- Enables Lambda Expressions
- Less code
- Better readability
- Supports Functional Programming
- Backward compatibility using default methods

### Interview Answer

**A Functional Interface is an interface that contains exactly one abstract method. It is mainly used with Lambda Expressions. It can also have multiple default and static methods.**

# Static Methods in Interface

Java 8 allows interfaces to have **static methods**.

A static method must have a body and belongs to the interface itself, not to its implementing classes.

### Syntax

```java
interface MyInterface {

    static void show() {
        System.out.println("Static Method");
    }
}
```

### Calling Static Method

Static methods can only be called using the interface name.

```java
MyInterface.show();
```

### Rules

- Static methods must have a body.
- Static methods cannot be overridden.
- Static methods can only be called using the interface name.
- Static methods cannot be called using an object reference.
- Implementing classes cannot directly access interface static methods.
- If an implementing class creates a static method with the same name, both methods are independent.

### Example

```java
interface MyInterface {

    static void show() {
        System.out.println("Interface Static Method");
    }
}

class Demo implements MyInterface {

    static void show() {
        System.out.println("Class Static Method");
    }
}

public class Main {
    public static void main(String[] args) {

        MyInterface.show();
        Demo.show();
    }
}
```

### Output

```text
Interface Static Method
Class Static Method
```

> Both methods are different. The class method does not override the interface static method.

### Main Method Inside Interface

Since Java 8, we can also write a `main()` method inside an interface.

```java
interface Test {

    public static void main(String[] args) {
        System.out.println("Main Method Inside Interface");
    }
}
```

### Key Points

- Introduced in Java 8.
- Static methods must have a body.
- Cannot be overridden.
- Called using interface name only.
- Interface and class static methods are independent.
- Main method can be written inside an interface.

### Interview Answer

**Java 8 allows static methods inside interfaces. These methods must have a body, cannot be overridden, and can only be called using the interface name.**

