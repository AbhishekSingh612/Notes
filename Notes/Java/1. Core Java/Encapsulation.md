Encapsulation is **bundling data and methods that work on that data within one unit**. It is a mechanism provided by some OOP languages like Java, C++, C# and it uses various techniques like private, protected, public etc. access modifiers to hide the data and provide a controlled way of accessing it. The main goal of encapsulation is to protect the internal data of the objects so that it cannot be accessed or modified by an external part of the program.

#### Code Example: 
```java
class BankAccount {  
    /* Data Hiding: The balance variable  
     * is hidden from external code  
     */  
    private double balance;   
  
    /* Encapsulation: The deposit and  
     * withdraw methods provide controlled  
     * access to the balance variable  
     */  
    public void deposit(double amount) {  
        this.balance += amount;  
    }  
  
    public void withdraw(double amount) {  
        if (amount <= this.balance) {  
            this.balance -= amount;  
        } else {  
            System.out.println("Insufficient  
            balance.");  
        }  
    }  
  
    /* Encapsulation: The getBalance method  
     * provides controlled access to   
     * the balance variable  
     */  
    public double getBalance() {  
        return this.balance;  
    }
```


#### Data Hiding: 
Data hiding refers to the **practice of hiding the internal state and implementation of an object, and exposing only the public interface to the outside world.** In this example, data hiding is used to protect the balance variable, by making it private so that it cannot be accessed directly by external code.

#### Difference between Data Hiding and Encapsulation
- Encapsulation is a mechanism to achieve data hiding. 
- Encapsulation is a way of enforcing the data hiding by providing the access modifiers like private, protected and public to the data fields and member functions. 
- Encapsulation also provides a way to provide controlled access to the data by using Getter and Setter method. 
- Data Hiding is a technique or practice of hiding the internal data of an object, whereas encapsulation is the mechanism provided by programming languages to enforce the data hiding and provide controlled way of accessing it