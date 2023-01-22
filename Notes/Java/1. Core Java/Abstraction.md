Abstraction is a fundamental concept in object-oriented programming (OOP) that refers to **the process of representing essential features of an object, while hiding the implementation details**. Abstraction helps to simplify complex systems by focusing on the essential features and ignoring the non-essential details.

#### Importance:
The significance of abstraction in OOP is that it allows developers to create *reusable*, *modular*, and *flexible* code by **separating the interface (what the object does) from the implementation (how the object does it).** This helps to reduce the complexity of a system, and to increase the *maintainability* and *scalability* of a program.

#### Real-World Example: 
- A car is an abstract class that has a method called `startEngine()`.  
- A gasoline car is a subclass of car that overrides the `startEngine()` method to start a gasoline engine.  
- An electric car is a subclass of car that overrides the `startEngine()` method to start an electric motor.
Here abstraction is hiding the internal complex details from the user of the Car type object, as user just have to call `startEngine()` without worrying about the implementation details 

#### Ways of achieving abstraction in Java
1. **Abstract classes**: An abstract class is a class that cannot be instantiated, but can be subclassed. An abstract class can have abstract methods (methods with no implementation) and non-abstract methods (methods with an implementation). Abstract methods must be overridden by the subclasses, and non-abstract methods can be inherited by the subclasses.  
2. **Interfaces**: An interface is a type that defines a set of abstract methods and constants. An interface does not have any implementation, but it can be implemented by a class. A class that implements an interface must implement all of the abstract methods and constants defined in the interface.

#### Abstract classes vs Interface:

1. **Abstract Class**:
	- Can have both abstract and non-abstract methods.
	- Can have instance variables and constructors.
	- Can only extend one abstract class.
	- Represent objects that have a common base class, but have different implementations.
		- **Example:** Vehicle is an abstract class, Car and Bike are subclasses of vehicle
1. **Interfaces**: 
	- Can only have abstract methods. 
	- Cannot have instance variables (only constants) or constructors.
	- Can implement multiple interfaces.
	- Represent objects that have unrelated behaviors, but need to implement a common set of methods. 
		- **Example:** Movable and Flyable are interfaces, Airplane and Bird implement these interfaces