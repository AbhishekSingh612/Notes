## Lambda Expression
A lambda expression is a way to write a function or method in a more concise and expressive way in Java 8. It is an anonymous function that can be passed as an argument or assigned to a variable. The basic syntax of a lambda expression is: 
```java
(parameters) -> { function body }
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

**Syntax :**
1. We can Omit parameter types for type inference: 
	`(s, i) -> s.length() > i`
2. We can Omit `()` for single parameter:
	`s -> s.length()`
3. We can Omit `{}` , semicolon `;` and `return` for single statement: 
	`() -> System.currentTimeMillis()` 

**Rules :**
1. Name of Parameter or any variable declared inside lambda cannot be same as any local variable 
2. Local Variable refferenced inside lambda must be final or Effectively final (Variable Not declared final, But is never reassigned) i.e. cannot reassign a value to local variable (neither inside lambda or outside)
3. No restriction on instance variable
4. **Reason :** Ease in performing concurrency operations and promotes functional programming and demotes imperative programming
~~~JAVA
int globalInt = 12;
public void localMethod() {  
    int localInt = 10;  
    MyObject obj = new MyObject();  
    Function<Integer, Integer> lambdaFuntion = () -> {  
        //int localInt;          // Invalid  
        //localInt = 100;        // Invalid   
        //obj = new MyObject();  // Invalid 
         
        obj.value = 20;          // Valid  
        int globalInt = 14;      // Valid
        globalInt = localInt;    // Valid
        return obj.value;  
    };
	//localInt = 100;            // Invalid
	
	// Instance variable has no restriction
	Consumer<Integer> globalEx = globalInt -> System.out.println(globalInt);
	Supplier<Integer> globalEx2 = () -> {
		int globalInt = 25;
		return globalInt;
	};
}	
~~~

**Internal Working:**
Java compiler generates an anonymous class that implements the functional interface. The generated class overrides the single abstract method with the code from the lambda expression. At runtime, the JVM creates an instance of this generated class and calls the overridden method when it is invoked. 

Local variables used inside lambda must be *final or effectively final* because :-
1. **Capturing local variables:** local variables are stored in stack and lambda might be executed after this local variable is no longer available. Hence java captures the local variable (makes copy of local variable value) so that this lambda can live outside the method
2. **Concurrency issue:** if non-final variable was allowed, value of the captured variable might change by the time lambda is executed, This will cause unexpected behaviour and hard to debug errors. Consider following example
	```java
	List<Integer> list = Arrays.asList(1, 2, 3);
	int sum = 10;
	list.forEach(i -> sum += i);	
	```
	Here if `sum` was not final or effectively final, and if the value of `sum` might have changed by the time the lambda is executed, the final value of `sum` would be different from what we expect.
	
	Also, it can also cause race conditions, which occurs when multiple threads access the same variable concurrently, and the final value of the variable depends on the order in which the threads execute. This can lead to unexpected and non-deterministic behavior.
	```java
	public void localVariableMultithreading() {
	    int start = 0;
	    executor.execute(() -> {
	        start++; 
	    }); 
	}
	```

Tags:: #java #java8 #lambdaExpressions #functionalInterface 

## Reference: 
https://www.baeldung.com/java-lambda-effectively-final-local-variables