Definition:  
Dependency Injection is a design pattern in which an object's dependencies are provided externally instead of being created internally by the object itself. The purpose of this pattern is to promote loose coupling, improve testability, and increase modularity in an application.

&nbsp;

Scenario:  
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
(For a better understanding of Object Oriented Design Rules refer to: https://github.com/Ali-Panjwani/Design-Defects-and-Restructuring-Resources/blob/main/Object%20Oriented%20Concepts.md)

&nbsp;

Problem:  
- Example Code:  
```
public class Email {
  public void SendEmail() {
    // code
  }
}

public class Notification {
  private Email _email;
  
  public Notification() {
    _email = new Email();
  }

  public void PromotionalNotification() {
    _email.SendEmail();
  }
}
```  
- Issues in the code:
1. Tight coupling: Difficult to replace or modify the Email class without affecting the Notification class.
2. Lack of abstraction: Email class exposes its implementation details to the Notification class, violating the principle of abstraction. (Exposes Implementation ->  other classes or components can directly access or manipulate the inner workings of that class.)  

&nbsp;

- Another aproach is:
```
public interface IMessageService {
  void SendMessage();
}

public class Email : IMessageService {
  public void SendMessage() {
    // code
  }
}

public class Notification {
  private IMessageService _iMessageService;

  public Notification() {
    _iMessageService = new Email();
  }
  
  public void PromotionalNotification() {
    _iMessageService.SendMessage();
  }
}
```
But still the problem is Lack of abstraction.

&nbsp;

Possible Solutions:
- Contructor Injection:
```
public class Notification {
  private IMessageService _iMessageService;

  public Notification(IMessageService _messageService) {
    this._iMessageService = _messageService;
  }

  public void PromotionalNotification() {
    _iMessageService.SendMessage();
  }
}

static void Main(string[] args) {
    IMessageService emailService = new Email();
    Notification notification = new Notification(emailService);
    notification.PromotionalNotification();
}
```
In the code above, the `Notification` class depends on an abstraction `IMessageService` rather than a concrete implementation `Email`. The dependency is injected into the `Notification` class through its constructor `public Notification(IMessageService _messageService)`, which makes it easier to modify or extend the code without affecting other parts of the system.  


The `PromotionalNotification` method still works the same way, as it calls the `SendMessage` method on the `IMessageService` object.

&nbsp;

- Property Injection:
```
public class Notification {
  public IMessageService MessageService {
    get;
    set;
  }

  public void PromotionalNotification() {
    if (MessageService == null) {
      // some error message
    } else {
      MessageService.SendMessage();
    }
  }
}

public static void main(String[] args) {
    Notification notification = new Notification();
    notification.setMessageService(new Email());
    notification.promotionalNotification();
}
```
The use of the `MessageService` property allows for more flexibility in setting the service at runtime. This means that the implementation can be changed without recompiling the code, which makes it easier to maintain and update.

&nbsp;

- Method Injection:
```
public class Email : IMessageService {
  public void SendMessage() {
    // code for the mail send
  }
}

public class SMS : IMessageService {
  public void SendMessage() {
    // code for the sms send
  }
}

public class Notification {
  public void PromotionalNotification(IMessageService _messageService) {
    _messageService.SendMessage();
  }
}

public static void main(String[] args) {
    Notification notification = new Notification();
    
    IMessageService emailService = new Email();
    notification.PromotionalNotification(emailService);

    IMessageService smsService = new SMS();
    notification.PromotionalNotification(smsService);
}
```
Better separation of concerns and adherence to the Single Responsibility Principle lead to modular and easy-to-reason-about code by separating the responsibility of object creation from their use.  

In this code, the creation of the `Email` service and the `SMS` service objects are separated from their use in the `Notification` class. The `Notification` class has a single responsibility of sending promotional notifications, and it does not concern itself with how the notifications are being sent.

&nbsp;

When to use:  
Dependency Injection is commonly used when a class has dependencies on other objects or services, and we want to decouple the class from those dependencies.  
It is particularly useful when:

1. The dependencies of a class may change over time.
2. The class has many dependencies and it is difficult to manage them manually.
3. The class needs to be tested in isolation from its dependencies.
4. The class has dependencies that are expensive to create or obtain.
