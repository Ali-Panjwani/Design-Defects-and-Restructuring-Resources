Class A uses Class B => Class A depends on services of Class B  
Implementation alternatives:
- Class A composes Class B and creates instance of class B -> That’s tightly coupled; Class A knows a LOT about class B
- Create an interface/abstract-class to encapsulate class B services;  
  Let class A create the concrete class and then user the interface -> Somewhat better; still Class A is creating the concrete class.
  
Explaination:  
When Class A uses Class B, it means that Class A relies on Class B to provide certain services. There are different ways to implement this dependency, but some approaches can lead to tight coupling, which means that Class A knows too much about Class B and can be hard to maintain.

One solution to avoid tight coupling is to create an interface or abstract class that encapsulates the services provided by Class B. This allows Class A to rely on the interface rather than on the implementation details of Class B. However, if Class A is responsible for creating an instance of the concrete class, it is still tightly coupled to Class B.

Questions:  
- How Class A knows too much about Class B and can be hard to maintain ?  
When Class A knows too much about Class B, it means that there is a high level of dependency between the two classes. This can make it harder to maintain the software over time, because any changes to Class B may also require changes to Class A, and vice versa.
  
- Whats the harm in making concrete class ?  
When Class A creates an instance of the concrete class (i.e., Class B), it is tightly coupled to Class B, which means that any changes to Class B can potentially affect Class A. This can make the code more fragile and harder to maintain over time.
```
// Interface that encapsulates the services provided by Class B
public interface ServiceB {
    public void method1();
}

// Concrete implementation of ServiceB
public class ClassB implements ServiceB {
    public void method1() {
        // implementation
    }
}

// Class A uses ServiceB through the interface, rather than the concrete implementation
public class ClassA {
    private ServiceB serviceB;

    public ClassA(ServiceB serviceB) {
        this.serviceB = serviceB;
    }

    public void doSomething() {
        // Use ServiceB through the interface
        serviceB.method1();
    }
}

// Usage:
ServiceB serviceB = new ClassB(); //Instantiating the Object
ClassA classA = new ClassA(serviceB);
classA.doSomething();
```
