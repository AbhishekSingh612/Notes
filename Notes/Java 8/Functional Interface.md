## Functional Interface

A functional interface is an interface in Java that has **exactly one abstract method**. It can have any number of default and static methods. 

A functional interface can be annotated with the `@FunctionalInterface` annotation, which is optional but helps to ensure that the interface is designed as a functional interface.

Some examples of functional interfaces in the Java standard library are `Runnable`, `Callable`, `Comparator`, `Consumer`, `Supplier` and many others.

Functional interfaces are used as the basis for lambda expressions and method references in Java 8. It can be used as the type for a lambda expression or method reference, which can be assigned to a variable, passed as an argument to a method, or returned from a method.

## Important Functional Interfaces in Java

There are several important functional interfaces in Java, but some of the most commonly used ones include:

1. **`java.util.function.Consumer<T>`**: Represents a function that takes in a single argument and returns no result.
    ```java
    Consumer<String> printConsumer = s -> System.out.println(s);
    printConsumer.accept("Hello World!");
    ```
2. **`java.util.function.Supplier<T>`**: Represents a function that takes no arguments and returns a result.
    ```java
    Supplier<LocalDate> dateSupplier = LocalDate::now;
    LocalDate date = dateSupplier.get();
    ```
3. **`java.util.function.Function<T, R>`**: Represents a function that takes in a single argument and returns a result.
    ```java
    Function<String, Integer> parseInt = Integer::parseInt;
    int number = parseInt.apply("123");
    ```
4. **`java.util.function.Predicate<T>`**: Represents a function that takes in a single argument and returns a boolean.
    ```java
    Predicate<String> isEmpty = s -> s.isEmpty();
    boolean result = isEmpty.test("Hello World");
    ```

