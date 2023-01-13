## Lambda Expression
A lambda expression is a way to write a function or method in a more concise and expressive way in Java 8. It is an anonymous function that can be passed as an argument or assigned to a variable. The basic syntax of a lambda expression is: 
```java
(parameters) -> function body
```

**Examples:**
```java 
(String s, int i) -> {
   int result = 0;
   for(int j = 0; j < s.length(); j++) {
       result += s.charAt(j);
   }
   return result > i;
}
```

```java 
() -> {
    System.out.println("Hello World!");
    System.out.println("Lambda expressions are fun!");
}

```

**Rules:**
1. We can Omit parameter types for type inference: `(s, i) -> s.length() > i`
2. We can Omit `()` for single parameter: `s -> s.length()`
3. We can Omit `{}` , semicolon `;` and `return` for single statement, `() -> System.currentTimeMillis()` 

**Internal Working:**
Java compiler generates an anonymous class that implements the functional interface. The generated class overrides the single abstract method with the code from the lambda expression. At runtime, the JVM creates an instance of this generated class and calls the overridden method when it is invoked. 


