Polymorphism is a fundamental concept in object-oriented programming (OOP) that refers to the **ability of a class or object to take on multiple forms**. Polymorphism **allows a class or object to behave in different ways in different contexts**, depending on the data or methods that are being used.

#### Types:
1. **Static Polymorphism** : This type of polymorphism, also known as **compile-time polymorphism or overloading,** occurs when a class or object has ==multiple methods or constructors with the same name, but with different signatures== or parameter lists. Static polymorphism allows a class or object to perform different actions depending on the **number or type of arguments** that are passed to a method.
2. **Dynamic Polymorphism** : This type of polymorphism, also known as **runtime polymorphism or overriding**, occurs when a ==subclass overrides a method that is inherited from a superclass==. Dynamic polymorphism allows a subclass to provide its own implementation of a method that is inherited from a superclass, and to execute that implementation at runtime.

#### Real-world Example
- Like a man can have different relation with different person like son, brother, husband, father 

#### Code Example
```java
class Animal {  
    public void eat() {  
        System.out.println("Eating...");  
    }  
      
    public void eat(String food) {  
        System.out.println("Eating " + food + "...");  
    }  
}  
  
class Dog extends Animal {  
    @Override  
    public void eat() {  
        System.out.println("Dog is eating...");  
    }  
      
    public void eat(String food, int numBones) {  
        System.out.println("Dog is eating " + food + " and crunching " + numBones + " bones...");  
    }  
}  
  
class Main {  
    public static void main(String[] args) {  
        Animal animal = new Animal();  
        animal.eat(); // prints "Eating..."  
        animal.eat("meat"); // prints "Eating meat..."  
          
        Dog dog = new Dog();  
        dog.eat(); // prints "Dog is eating..."  
        dog.eat("meat", 2); // prints "Dog is eating meat and crunching 2 bones..."  
    }  
}
```