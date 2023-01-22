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
    
    Relate Functional Interface :-
     - `BiConsumer<T,U>` which takes 2 inputs of T and U type

2. **`java.util.function.Supplier<T>`**: Represents a function that takes no arguments and returns a result.
    ```java
    Supplier<LocalDate> dateSupplier = LocalDate::now;
    LocalDate date = dateSupplier.get();
    ```
    
3. **`java.util.function.Function<T, R>`**: Represents a function that takes in a single argument and returns a result. Also, contains some useful default methods - `compose(Function before)` and `andThen(Function after)`.
    ```java
    Function<String, Integer> parseInt = Integer::parseInt;
    int result = parseInt.apply("123"); // Integer : 123

	// First ParseInt then multiply 10
    Function<Integer, Integer> multiply10 = i -> i*10;
    result = parseInt.andThen(multiply10).apply("123"); // Integer : 1230
    
    // First ParseInt then multiply 10
    Function<String, String> addZero = s -> s.concat("0");
    result = parseInt.compose(addZero).apply("123"); // Integer : 1230
     
    ```
    
    Related Functional Interface :-
	1. `BiFunction<T,U,R>` which has 2 input of T and U type
	2. `UnaryOperator<T> implements Function<T,T>` Here input and ouput are of same type
	3. `BinaryOperator<T> implements BiFunction<T,T,T>` Here 2 inputs and output is of Type T

4. **`java.util.function.Predicate<T>`**: Represents a function that takes in a single argument and returns a boolean. Also, cantains some useful default methods - `and()`, `or()`, `negate()`
    ```java
    Predicate<String> isEmpty = s -> s.isEmpty();
    Predicate<String> has6PlusLength = s -> s.isEmpty();
    
    boolean andResult = isEmpty
				    .and(has6PlusLength) // Returns Lambda with `and` of both
				    .test("Hello World");

	boolean orResult = isEmpty
				    .or(has6PlusLength)// Returns Lambda with `or` of both
				    .test("Hello World");
				    
	boolean negResult = isEmpty
				    .negate()// Returns Lambda with negate of result
				    .test("Hello World");

    ```
	
	Related Functional Interface :-
	- `BiPredicate<T,U>` accepts 2 inputs and produce boolean


Tags:: #java #java8 #functionalInterface