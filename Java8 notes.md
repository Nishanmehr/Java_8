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

# Using Lambda Expression with Predefined Functional Interfaces

### 1. Runnable Interface

`Runnable` is a predefined Functional Interface available in Java.
```java
void run();
```

So, it can be implemented using a Lambda Expression.

## Example

```java
Runnable r = () -> System.out.println("Thread is running");

r.run();
```

## Using Thread

```java
Thread t = new Thread(
    () -> System.out.println("Thread is running")
);

t.start();
```

## Key Points

- Predefined Functional Interface.
- Contains one abstract method `run()`.
- Used for multithreading.
- Lambda removes anonymous class code.
- Makes code short and readable.



# Comparator Interface

`Comparator` is a predefined Functional Interface used for custom sorting.

It contains one abstract method:

```java
int compare(T o1, T o2);
```

So, it can be implemented using a Lambda Expression.

### Example

```java
List<Integer> list = Arrays.asList(50, 10, 40, 20);

Collections.sort(list, (a, b) -> a - b);

System.out.println(list);
```

### Output

```text
[10, 20, 40, 50]
```

### Descending Order

```java
Collections.sort(list, (a, b) -> b - a);
```

### Key Points

- Predefined Functional Interface.
- Used for custom sorting.
- Contains one abstract method `compare()`.
- Lambda makes sorting code short and readable.
- Returns:
  - Negative → First object comes first.
  - Positive → Second object comes first.
  - Zero → Both are equal.

# Lambda Expression vs Anonymous Class 

### Employee Class

```java
class Employee {
    int id;
    String name;

    Employee(int id, String name) {
        this.id = id;
        this.name = name;
    }

    @Override
    public String toString() {
        return id + " " + name;
    }
}
```

### Using Anonymous Class
```java
List<Employee> employees = Arrays.asList(
        new Employee(103, "Rohit"),
        new Employee(101, "Aman"),
        new Employee(102, "Neha")
);

Collections.sort(employees, new Comparator<Employee>() {
    @Override
    public int compare(Employee e1, Employee e2) {
        return e1.id - e2.id;
    }
});

System.out.println(employees);
```
### Using Lambda Expression
```java
List<Employee> employees = Arrays.asList(
        new Employee(103, "Rohit"),
        new Employee(101, "Aman"),
        new Employee(102, "Neha")
);

Collections.sort(employees,
        (e1, e2) -> e1.id - e2.id);

System.out.println(employees);
```

### Output
```text
[101 Aman, 102 Neha, 103 Rohit]
```
### Observation
Anonymous Class:

```java
new Comparator<Employee>() {
    @Override
    public int compare(Employee e1, Employee e2) {
        return e1.id - e2.id;
    }
}
```
Lambda:

```java
(e1, e2) -> e1.id - e2.id
```

The logic is the same, but Lambda removes unnecessary code and makes it more readable.

# Predicate Interface

`Predicate` is a predefined Functional Interface introduced in Java 8.

It contains only one abstract method and can have multiple default and static methods.

A Predicate is used to test a condition and always returns a boolean value (`true` or `false`).

## Abstract Method

```java
boolean test(T t);
```

## Example

```java
Predicate<Integer> p = num -> num > 10;

System.out.println(p.test(15));
System.out.println(p.test(5));
```

## Output

```text
true
false
```

# Important Methods

## 1. and()

Used to combine two predicates.

Returns `true` only if both conditions are satisfied.

```java
Predicate<Integer> p1 = n -> n > 10;
Predicate<Integer> p2 = n -> n % 2 == 0;

Predicate<Integer> result = p1.and(p2);

System.out.println(result.test(20));
```

### Output

```text
true
```

---

## 2. or()

Returns `true` if at least one condition is satisfied.

```java
Predicate<Integer> result = p1.or(p2);
```

---

## 3. negate()

Returns the opposite result.

```java
Predicate<Integer> p = n -> n > 10;

System.out.println(p.negate().test(15));
```

### Output

```text
false
```

---

## 4. isEqual()

Used to check equality.

```java
Predicate<String> p = Predicate.isEqual("Java");

System.out.println(p.test("Java"));
```

### Output

```text
true
```

## Key Points

- Introduced in Java 8.
- Predefined Functional Interface.
- Represents a boolean condition.
- Contains `test()` method.
- Returns `true` or `false`.
- Supports `and()`, `or()`, `negate()`, and `isEqual()` methods.

## Interview Answer

**Predicate is a Functional Interface introduced in Java 8 that represents a condition. It contains the `test()` method and returns a boolean value (`true` or `false`).**

# Function Interface

`Function` is a predefined Functional Interface introduced in Java 8.

It takes an input, performs some operation, and returns a result.

The input and return type can be anything such as `Integer`, `String`, `Double`, etc.

## Abstract Method

```java
R apply(T t);
```

## Example

```java
Function<Integer, Integer> square = n -> n * n;

System.out.println(square.apply(5));
```

## Output

```text
25
```

# Important Methods

## 1. andThen()

Executes the current function first and then the next function.

```java
Function<Integer, Integer> fun1 = n -> n * 2;
Function<Integer, Integer> fun2 = n -> n + 10;

System.out.println(fun1.andThen(fun2).apply(5));
```

### Flow

```text
5 -> fun1 -> 10 -> fun2 -> 20
```

### Output

```text
20
```

---

## 2. compose()

Executes the second function first and then the current function.

```java
Function<Integer, Integer> fun1 = n -> n * 2;
Function<Integer, Integer> fun2 = n -> n + 10;

System.out.println(fun1.compose(fun2).apply(5));
```

### Flow

```text
5 -> fun2 -> 15 -> fun1 -> 30
```

### Output

```text
30
```

---

## 3. identity()

Returns the same value that is passed as input.

```java
Function<String, String> fun = Function.identity();

System.out.println(fun.apply("Java"));
```

### Output

```text
Java
```

## Key Points

- Introduced in Java 8.
- Predefined Functional Interface.
- Contains `apply()` method.
- Takes input and returns output.
- `andThen()` → First current function, then next function.
- `compose()` → First second function, then current function.
- `identity()` → Input = Output.

## Interview Answer

**Function is a Functional Interface that takes an input, performs an operation, and returns a result. It contains the `apply()` method and provides methods like `andThen()`, `compose()`, and `identity()`.**















