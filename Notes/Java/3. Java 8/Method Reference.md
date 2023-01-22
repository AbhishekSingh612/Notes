# Method Reference

A method reference is a **shorthand notation for a lambda expression** that references an existing method by name. It is used to pass a method as an argument to another method, without having to create a lambda expression that invokes the method. 

The syntax for a method reference is `ClassName::methodName` or `objectName::methodName`. This method can be static or non-static incase of both class or object 

## Example

~~~java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
//numbers.forEach((i)->System.out.println(i));
numbers.forEach(System.out::println); //Method Reference Equivalent
~~~

In this example, `println` is a static method of the `System.out` class, and the method reference `System.out::println` is used to pass it as an argument to the `forEach` method of the `List` interface.

## Where and How to use

Method references can be used in any place where a lambda expression can be used.  Method references can be used with both static and non-static methods and with both class and instance methods. 

There are 4 types of method references:
1. **Reference to a static method**
~~~java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
numbers.forEach(System.out::println);
~~~

2. **Reference to an instance method of a particular object**
~~~java
String str = "Hello";
Consumer<String> printString = str::toUpperCase;
printString.accept(str);
~~~

3. **Reference to an instance method of an arbitrary object of a particular type**
~~~java
List<String> words = Arrays.asList("Hello", "world");
words.sort(String::compareToIgnoreCase);
~~~

4. **Constructor Reference**
~~~java
// Supplier<Student> supplier = () - > new Student();
Supplier<Student> supplier = Student::new;
Student s = supplier.get();

// With arguments : (String name) -> new Student(name); 
Function<String,Student> supplier2 = Student::new;
Student s2 = supplier2.apply("Abhishek");

// Another Example
List<String> names = Array.asList("Ankur","Abhishek","Ashok");
Student[] students = names.stream()
						  .map(Student::new)
						  .toArray(Student[]::new);
~~~


Method references can be used to simplify the code, making it more readable and maintainable. They are widely used in functional programming with Streams, Iterators and other functional interfaces.


Tags:: #java #java8 #methodReference #lambdaExpressions 