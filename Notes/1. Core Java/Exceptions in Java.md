```
	              ---> Throwable <--- 
	              |    (checked)     |
	              |                  |
	              |                  |
	      ---> Exception           Error
	      |    (checked)        (unchecked)
	      |
	RuntimeException
	  (unchecked)
```

An **Exception** is an event that occurs during the execution of a program that disrupts the normal flow of instructions. Exceptions are objects of the class `Throwable` and its subclasses.


### Types of Exception

 There are 3 types of Exception: 
 1. Checked Exception
 2. Unchecked / Runtime Exception
 3. Error

#### Checked Exception
 - These exceptions are checked at compile-time. That means, if a method throws a checked exception, it must either handle the exception using `try-catch` or declare it in the method signature using the `throws` keyword. 
 - The idea behind checked exceptions is to force the developer to think about and handle exceptional situations that may occur during the execution of a program. 
 - Examples of checked exceptions include IOException, SQLException, and FileNotFoundException.
 - If the exception is recoverable, meaning that the program can continue to execute after handling the exception, it is generally considered a checked exception.

#### Unchecked Exception
 - These are exceptions that are not checked at compile-time. That means, the compiler does not force the developer to handle or declare them. 
 - Unchecked exceptions are typically caused by programming errors, such as null pointer exceptions, index out of bounds exceptions, and illegal argument exceptions. These are considered as bugs in the program and are usually handled by the Java runtime system. 
 - Examples of unchecked exceptions include NullPointerException, ArrayIndexOutOfBoundsException, and IllegalArgumentException.
 - These are exceptional conditions that are internal to the application, and that the application usually cannot anticipate or recover from

#### Error
 - These are exceptional conditions that are external to the application and that the application usually cannot anticipate or recover from. 
 - These are unchecked (not checked by compiler). Hence we are not forced to handle them (and typically we would not)
 - Suppose program opens a file successfully but is unable to read its content due to hardware or system malfunction. The unsuccessfull read will throw `IOError` 
 - Examples of errors include OutOfMemoryError and StackOverflowError.
```java
//Custom Checked Exception Example
public class CustomCheckedException extends Exception { 
	public CustomCheckedException(String message) {
		super(message); 
	} 
}

//Custom Unchecked Exception Example
public class CustomUncheckedException extends Exception { 
	public CustomUncheckedException(String message) {
		super(message); 
	} 
}
```

### Handling Exception
 Mechanism to handle exception so that normal flow of application can be maintained is called Exception handling.
 
 We can handle exception using :-
 1. Throws keyword
 2. try-catch block

#### Throws keyword
 - `throws` keyword is used to declare an exception. It indicated that this method might throw one of the listed type of exception.
 - The caller of this method has to handle this exception (either using throws or try-catch) 
 - If our method throws a checked exception it is madatory to declare it using `throws` keyword. For unchecked it is optional (typically avoid declaring unchecked Exception as they are unrecoverable and not meant to be handled) 
   ```java
   public void getFileContent() throws FileNotFoundException {
	   Scanner contents = new Scanner(new File(playerFile)); 
	   return Integer.parseInt(contents.nextLine());
   }
   ```

### Try-Catch block
 If we want to handle the exception ourself we can use try catch block. We can either rethrow the exception in catch block or perform recovery steps.
 ```java
 try{
	 //some code that might throw exception
 } catch(Exception e){
	 //steps to perform if exception occurred 
 }
 ```

 1. **Try** : 
  - try is used to enclose the 'risky' code that might throw an exception
  - try must be followed by either catch or finally (try cannot exist alone)
  - Note : Any statement in try block after the exception will not execute. So it is recommended to keep only risky code inside try block
 2. **Catch :**
  - It is used to handle the exception occurred in the try block. Here we might perform recovery steps or rethrow the exception
  - We can have multiple catch blocks but we must define more specific (subclass) exceptions first else java will consider exception is already handled and give compile time error 
  - After java 7 we can also Union multiple exceptions in single catch block using `|` 
 3. **Try with resources :**
  - Introduced in java 7, we can define Resource that implements AutoClosable interface within round brackets. Java will automatically close this resource after we are done with it
  - We can define multiple resource seperated by semi-colon, resource defined first is closed at last
  - After java 9, instead of defining new variable for resource within try with resource we use effectively final resource variables like `try(scanner; writter) {}`
```java
public int getPlayerScore(String playerFile) {
	// try with resource
	try (Scanner contents = new Scanner(new File(playerFile)) 
	//; someOtherResource ) 
	{
		int result = Integer.parseInt(contents.nextLine());
		//Any code after risky line 
		 //will not execute incase of exception
        return result;
    } 
    // Multiple catch block - from specific to more generic
    catch (FileNotFoundException e) 
    {
        logger.warn("File Not found!!", e);
        return 0;
    } 
    // Union of Exceptions
    catch (IOException | NumberFormatException e) {
        logger.warn("Failed to load score!", e);
        return 0;
    }
}
```

 4. **Finally :**
  - It is used to execute the code that must execute regardless of whether an exception occurs or not. It is executed even if we are rethrowing exception or returning in catch block  
  - It is used to execute some important code that must execute not matter what like closing file, closing db connection, cleaning temp file.
### Throwing Exception 
 - We can throw an exception using the `throw` keyword. 
 - For checked exception we have to declare that exception in method signature using throws as well.
 - For unchecked exception declaring is not needed
 - Special case: if our code inside try block only raises unchecked exception and we caught it as general Exception or Throwable and rethrow this Exception object, Now even though Exception is considered checked exception we dont need to declare it in signature as java can detect that checked exception is not possible
 - Sneaky throw: throwing checked exception as unchecked. It is possible ( after java 8) using a workaround, compiler infers throws T as RuntimeException type (Not recommended as we cannot handle the checked exception even if we want to using this approach as compiler throw error if we try saying No {Some Checked Exception} thrown by this code)
 ```java
 //Checked Exception
 public void foo()throws IOException //Declaring Exception
 {
	 if(/*Some condition*/)
		 throws new IOException();
	 
	 //some logic
 }

 //Unchecked Exception
 public void foo(String input)
 {
	 if(input==null)
		 throws new IllegalArgumentException();

	//some logic
 }

//Special case
 public void callFoo() //throws Exception not needed 
 {
	 try{
		 throw new NullPointerException();
	 } catch(Exception e) {
		 throw e;
	 }
 }


//Sneaky throw
 public static <E extends Throwable> void sneakyThrow(Throwable e) throws E { 
	throw (E) e; 
 }

 private static void throwSneakyIOException() { 
	sneakyThrow(new IOException("sneaky")); 
 }
```

### Overriding Risky methods
 1. If the parrent class method does not declare any exception then we can declare only unchecked exception in the child class method
 2. If the parent class method declares checked exception then we may declare same or sub-classes of that exceptions. In other words we can define more specific exception but not more generic one 
 ```java

//Imagine parent foo throws FileNotFoundException
//And Child foo throws IOException (super class of FileNotFound)

 Parent obj = new Child();
 obj.foo();

// foo can actually throw IOException but compiler will only tell us to catch FileNotFoundException which is wrong as IOException is more wider and can be due to some other exception like FileAlreadyExistException
```

### Anti-pattern
 1. **Error hiding or Exception swallowing**: catching an error or exception, and then continuing without logging, processing, or reporting the error to other parts of the software
	 1. Instead of empty catch block atleast write comment like "This exception will never happen"
	 2. Instead of just printing stacktrace, log.error("Define the problem", e) so that we can debug later
	 3. Avoid Losing actual cause of exception while rethrowing custom Exception instead wrap actual exception with your custom exception `catch(IOException e) { throws new CustomException(e); }`
 2. Avoid return or throw in finally block
 3. Avoid using throw as goto 
## Reference
https://www.baeldung.com/java-exceptions