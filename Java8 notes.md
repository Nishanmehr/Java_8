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

# Consumer Interface

`Consumer` is a predefined Functional Interface introduced in Java 8.

It accepts an input and performs an operation on it but does not return any value.

## Abstract Method

```java
void accept(T t);
```

> Consumer contains the `accept()` method, not `apply()`.

## Example

```java
Consumer<String> c = name -> System.out.println(name);

c.accept("Nishant");
```

## Output

```text
Nishant
```

# Important Method

## andThen()

Used to chain multiple Consumer operations.

```java
Consumer<String> c1 = s -> System.out.println(s);
Consumer<String> c2 = s -> System.out.println(s.toUpperCase());

c1.andThen(c2).accept("java");
```

### Output

```text
java
JAVA
```

## Key Points

- Introduced in Java 8.
- Predefined Functional Interface.
- Takes input and consumes it.
- Does not return any value.
- Contains `accept()` method.
- Supports `andThen()` for chaining operations.

## Interview Answer

**Consumer is a Functional Interface that accepts an input and performs an operation on it without returning any value. It contains the `accept()` method.**

# Supplier Interface

`Supplier` is a predefined Functional Interface introduced in Java 8.

It does not take any input and only supplies (returns) a value.

## Abstract Method

```java
T get();
```

## Example

```java
Supplier<String> s = () -> "Hello Java";

System.out.println(s.get());
```

## Output

```text
Hello Java
```

## Example 2

```java
Supplier<Integer> s = () -> 100;

System.out.println(s.get());
```

## Output

```text
100
```

## Key Points

- Introduced in Java 8.
- Predefined Functional Interface.
- Takes no input.
- Only provides output.
- Contains `get()` method.
- Opposite of Consumer.

## Interview Answer

**Supplier is a Functional Interface that does not take any input and only returns a value. It contains the `get()` method.**



# BiPredicate Interface

`BiPredicate` is a predefined Functional Interface introduced in Java 8.

It works like `Predicate`, but it accepts **two input values** instead of one and returns a boolean value (`true` or `false`).

When a condition needs to be checked on two inputs at the same time, we use `BiPredicate`.

## Abstract Method

```java
boolean test(T t, U u);
```

## Example

```java
BiPredicate<Integer, Integer> p =
        (a, b) -> a > b;

System.out.println(p.test(20, 10));
```

## Output

```text
true
```

## Important Methods

### and()

Returns `true` only if both conditions are satisfied.

```java
p1.and(p2);
```

### or()

Returns `true` if at least one condition is satisfied.

```java
p1.or(p2);
```

### negate()

Returns the opposite result.

```java
p.negate();
```

## Key Points

- Introduced in Java 8.
- Similar to Predicate.
- Accepts two input values.
- Returns `true` or `false`.
- Contains `test()` method.
- Supports `and()`, `or()`, and `negate()`.

## Interview Answer

**BiPredicate is a Functional Interface that accepts two input values, checks a condition, and returns a boolean value (`true` or `false`). It is used when a Predicate needs to work with two inputs.**


# BiFunction Interface

`BiFunction` is a predefined Functional Interface introduced in Java 8.

It works like `Function`, but it accepts **two input values** and returns a result.

## Abstract Method

```java
R apply(T t, U u);
```

## Example

```java
BiFunction<Integer, Integer, Integer> add =
        (a, b) -> a + b;

System.out.println(add.apply(10, 20));
```

## Output

```text
30
```

## Important Method

### andThen()

Used to perform another operation on the result returned by `BiFunction`.

```java
BiFunction<Integer, Integer, Integer> add =
        (a, b) -> a + b;

Function<Integer, Integer> square =
        n -> n * n;

System.out.println(add.andThen(square).apply(10, 20));
```

### Flow

```text
10 + 20 = 30
30 * 30 = 900
```

### Output

```text
900
```

## Key Points

- Introduced in Java 8.
- Similar to Function.
- Accepts two input values.
- Returns one output value.
- Contains `apply()` method.
- Supports `andThen()` method.

## Interview Answer

**BiFunction is a Functional Interface that accepts two input values, performs an operation, and returns a result. It contains the `apply()` method.**


# BiConsumer Interface

`BiConsumer` is a predefined Functional Interface introduced in Java 8.

It works like `Consumer`, but it accepts **two input values** and does not return any value.

It is generally used when an operation needs two inputs.

## Abstract Method

```java
void accept(T t, U u);
```

## Example

```java
BiConsumer<String, Integer> c =
        (name, age) -> System.out.println(name + " " + age);

c.accept("Nishant", 22);
```

## Output

```text
Nishant 22
```

## Important Method

### andThen()

Used to chain multiple BiConsumer operations.

```java
BiConsumer<String, Integer> c1 =
        (name, age) -> System.out.println(name);

BiConsumer<String, Integer> c2 =
        (name, age) -> System.out.println(age);

c1.andThen(c2).accept("Nishant", 22);
```

## Output

```text
Nishant
22
```

## Key Points

- Introduced in Java 8.
- Similar to Consumer.
- Accepts two input values.
- Does not return any value.
- Contains `accept()` method.
- Supports `andThen()` method.

## Interview Answer

**BiConsumer is a Functional Interface that accepts two input values and performs an operation without returning any value. It contains the `accept()` method.**


# UnaryOperator Interface

`UnaryOperator` is a predefined Functional Interface introduced in Java 8.

It is a special type of `Function` where the input type and return type are the same.

## Abstract Method

```java
T apply(T t);
```

## Example

```java
UnaryOperator<Integer> square =
        n -> n * n;

System.out.println(square.apply(5));
```

## Output

```text
25
```

## Example 2

```java
UnaryOperator<String> upper =
        str -> str.toUpperCase();

System.out.println(upper.apply("java"));
```

## Output

```text
JAVA
```

## Key Points

- Introduced in Java 8.
- Child Interface of `Function`.
- Takes one input.
- Returns one output.
- Input type and return type must be the same.
- Contains `apply()` method.

## Interview Answer

**UnaryOperator is a special type of Function interface where the input type and return type are the same. It contains the `apply()` method and is used to perform operations on a single value and return the same type of result.**

# BinaryOperator Interface

`BinaryOperator` is a predefined Functional Interface introduced in Java 8.

It is a special type of `BiFunction` where both input types and the return type are the same.

## Abstract Method

```java
T apply(T t1, T t2);
```

## Example

```java
BinaryOperator<Integer> add =
        (a, b) -> a + b;

System.out.println(add.apply(10, 20));
```

## Output

```text
30
```

## Example 2

```java
BinaryOperator<Integer> max =
        (a, b) -> a > b ? a : b;

System.out.println(max.apply(10, 20));
```

## Output

```text
20
```

## Key Points

- Introduced in Java 8.
- Child Interface of `BiFunction`.
- Takes two input values.
- Returns one output value.
- Both input types and return type must be the same.
- Contains `apply()` method.

## Interview Answer

**BinaryOperator is a special type of BiFunction where both input parameters and the return type are the same. It is used to perform operations on two values of the same type and return a result of the same type.**



# Method Reference (::)

Method Reference is a short form of a Lambda Expression.

It is used when a Lambda Expression only calls an existing method.

Instead of writing a lambda, we can directly refer to the method using the `::` operator.

## Syntax

```java
ClassName::methodName
```

## Example

### Using Lambda

```java
List<String> names = Arrays.asList("Java", "Python", "Spring");

names.forEach(name -> System.out.println(name));
```

### Using Method Reference

```java
List<String> names = Arrays.asList("Java", "Python", "Spring");

names.forEach(System.out::println);
```

## Output

```text
Java
Python
Spring
```

## Types of Method References

### 1. Static Method Reference

```java
ClassName::staticMethod
```

Example:

```java
Math::max
```

### 2. Instance Method Reference of an Object

```java
objectReference::methodName
```

Example:

```java
System.out::println
```

### 3. Instance Method Reference of a Class

```java
ClassName::methodName
```

Example:

```java
String::toUpperCase
```

### 4. Constructor Reference

```java
ClassName::new
```

Example:

```java
Supplier<String> s = String::new;
```

## Key Points

- Introduced in Java 8.
- Uses `::` operator.
- Short form of Lambda Expression.
- Improves readability.
- Used when Lambda only calls an existing method.

## Interview Answer

**Method Reference is a shorthand form of a Lambda Expression used to refer to an existing method or constructor using the `::` operator.**



# Constructor Reference (::new)

Constructor Reference is a special type of Method Reference used to call a constructor.

Instead of creating an object using a Lambda Expression, we can directly refer to the constructor using the `::new` operator.

## Syntax

```java
ClassName::new
```

## Using Lambda

```java
Supplier<User> s = () -> new User();
```

## Using Constructor Reference

```java
Supplier<User> s = User::new;
```

## Example

```java
class User {
    User() {
        System.out.println("User Object Created");
    }
}

public class Main {
    public static void main(String[] args) {

        Supplier<User> s = User::new;

        s.get();
    }
}
```

## Output

```text
User Object Created
```

## Why Use Constructor Reference?

- Less code
- Better readability
- Short form of Lambda Expression
- Used for object creation

## Key Points

- Uses `::new`.
- Special type of Method Reference.
- Refers to a constructor.
- Creates objects without writing Lambda code.
- Works with Functional Interfaces.

## Interview Answer

**Constructor Reference is a shorthand way to call a constructor using the `::new` operator. It is used to create objects in a cleaner and more readable way.**












