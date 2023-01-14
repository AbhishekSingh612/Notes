List.of returns immutable list where as Arrays.asList returns mutable but fixed size array
```java

List<Integer> asList = Arrays.asList(1, 2, 3); //Fixed Size
// asList.add(4);
// asList.remove();
asList.set(0, 0); //alowed as size remains fixed
asList.sort();
asList.contains(null); // OK

List<Integer> ofList = List.of(1, 2, 3);// Immutable
// ofList.add(4);
// ofList.remove();
// ofList.set(0, 0);
// ofList.sort();
// ofList.contains(null) // NPE
```