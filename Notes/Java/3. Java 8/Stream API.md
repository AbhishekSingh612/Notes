# Stream API

- **Stream** (`java.util.stream.Stream<T>`) is a sequence of elements which can be created out of collections or any other I/O resource. Example 
	```java
	Stream<String> nameStream = Stream.of("Abhishek", "Ankur", "Ashok");
    //OR
	List<String> names = Arrays.asList("Abhishek", "Ankur", "Ashok");
	Stream<String> nameStream = names.stream();
	```
- Can be performed sequentially using `stream()` or in parallel using `parallel()` on seq stream or `parallelStream()` on collections
- `java.util.stream` contains classes for proccessing sequence of elements
- Stream pipeline includes :-
	1. *Source or Stream Creation*: It takes collection or any other I/O resource and creates its Stream
	2. *Operations*: 
		1. *Intermediate*: Allows chaining i.e. It takes `Stream<T>` and outputs new `Stream<T>`. We can  have multiple intermediate operations.
		2. *Terminal*: It takes `Stream<T>` but returns result of definitive type and hence we can only use one terminal operation per stream pipeline. Additionally pipeline is only triggered after terminal operation is called.
- Any operation performed on stream is not reflected in the source
- It is
- *Lazy Invocation* : Intermediate operations are lazy. All intermediate operations are performed on the stream only when a terminal operation is invoked on it. Also they are executed only if it is necessary for terminal operation execution. Example findFirst() operation will terminate the stream as soon as it gets an element even though stream might have more elements
- *Terminal Short-circuit* : Terminal operation are those operation that can produce result before even processing the entire stream. `findFirst()`, `findAny()`, `allMatch()`,` anyMatch()`, and `noneMatch()`.
- *Order of Execution* is really important 
- Stream flow only in one direction and Stream object can be only referenced until terminal operation is not called. Once terminal operation is called we can no longer reference the stream

## 1. Stream Creation:
 We can create multiple stream from single source. Also note stream does not modify its source. There are many ways to create streams some of them are as follows:-
 1. Generate Stream from resource: 
	 1. `Stream.empty()` creates empty stream, Useful to handle null list
	 2. Collections `stream()` method creates stream of collection elements
	 3. `Stream.of(T... values)` creates stream of comma seperated values. Uses Arrays stream method internally.  Cannot directly pass single `null` use `new Object[]{null}`
	 4. `Arrays.stream(T[] array)` creates stream of input array. Array cannot be null but value inside it can be
	 5. `Stream.builder().add(T value) ... .build()` 
 2.  Generate Infinite Stream
	 1. `Stream.generate(Supplier<T>)` generates infinite stream using supplier
	 2. `Stream.iterate(T firstElement, UnaryOperator functionToGenNext)`
 3. Generate primitive stream `IntStream` , `LongStream`, `DoubleStream` ( More details later //TODO )
	 1. `range(int startInclusive, int endExclusive)` creates stream from start to end-1, incremented by 1. End is not included. (Not available in doubleStream)
	 2. `rangeClosed(int startInclusive, int endInclusive)` creates stream from start to end, incremented by 1. End is Included (Not available in doubleStream)
 4. Generate Stream for File
	 1. `Files.lines(Path)` returns Stream of String (containing individual lines)
 5. Combining two Stream 
	 1. `Stream.concat(Stream<? extends T>, Stream<? extends T>)` returns combination of both stream as `Stream<T>` 
    ```java
    // 1- To create empty stream
	 Stream<String> streamEmpty = Stream.empty();
	
	 // Empty stream use-case
	 // Avoid NPE when list is null
	 public Stream<String> streamOf(List<String> list) {
		return list == null ? Stream.empty() : list.stream(); 
	 }

	// 2- Using Collections stream method
	Collection<String> collection = Arrays.asList("a", "b", "c"); 
	Stream<String> streamOfCollection = collection.stream()

	// 3 - Using `of` method of Stream class
	Stream<String> streamOf = Stream.of("Test", null, "Test2");

	// 4 - Using `stream` method of Arrays class
	IntStream arrayStream = Arrays.stream(new int[]{1,3,4});

	// 5 - Using stream builder
	Stream<String> streamBuilder = Stream.String>builder()
									.add("a")
									.add("c").build();

	// 6 - Using `generate` method of Stream class
	Stream<String> streamBuilder = Stream.generate(()->"Abhishek")
									.limit(10);

	// 7 - Using `iterate` method of Stream class
	Stream<Integer> streamIterated = Stream.iterate(40, n -> n + 2)
									.limit(20); // 40 42 44 ....

	// 8 - Using range and rangeClosed for primitive types Stream
	IntStream intStream = IntStream.range(1,10); // 1 to 9
	IntStream intStream = IntStream.rangeClosed(1,10); // 1 to 10

	// 9 - Reading files using Files.lines()
	Path path = Paths.get("C:\\file.txt"); 
	Stream<String> lines = Files.lines(path); 
	Stream<String> lines2 = Files.lines(path, Charset.forName("UTF-8"));

	// 10 - Combine 2 stream
	Stream<String> lines3 = Stream.concat(lines, lines2);
	```

Tags:: #java #java8 #StreamAPI #lambdaExpressions #methodReference 

## Reference: 
https://www.scaler.com/topics/java/streams-in-java/
https://www.baeldung.com/java-8-streams