Definition:  
Define an interface for creating an object, but let subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses.  
Also Known As: Virtual Constructor

&nbsp;

Scenario:
- Consider a design framework where abstract classes Class A and Class D have a
aggregation relation whereby Class A creates instances of Class D.
- Since both classes A and D are abstract, they will be subclassed to provide
implementation.
- Since the knowledge about which subclass of D to instantiate is specific to subclass of A, at
an abstract level A cannot predict which subclass of D to create.

&nbsp;

Solution:  
Code:
```
// Abstract class for a document
abstract class Document {
  public abstract void open();
  public abstract void save();
  public abstract void close();
  public abstract void revert();
}

// Concrete class for a document of type MyDocument
class MyDocument extends Document {
  public void open() {
    System.out.println("Opening MyDocument...");
  }

  public void save() {
    System.out.println("Saving MyDocument...");
  }

  public void close() {
    System.out.println("Closing MyDocument...");
  }
  
  public void revert() {
    System.out.println("Reverting MyDocument...");
  }
}

// Abstract class for an application
abstract class Application {
  public abstract Document createDocument();
  public abstract void newDocument();
  public abstract void openDocument();
}

// Subclass of Application that realizes MyDocument
class MyApplication extends Application {
  public Document createDocument() {
    return new MyDocument();
  }
  
  public void newDocument() {
    Document doc = createDocument();
    doc.save();
    doc.close();
    }

  public void openDocument() {
    Document doc = createDocument();
    doc.open();
  }
}

// Example usage
public class Main {
  public static void main(String[] args) {
    Application myApp = new MyApplication();
    myApp.newDocument();
    myApp.openDocument();
  }
}
```

The `Document` and `Application` abstract classes define the required methods that need to be implemented by the concrete classes. The `MyDocument` class implements the Document interface and provides the actual implementation for the methods.  

Similarly, the `MyApplication` class implements the `Application` abstract class and provides the implementation for the `createDocument()`, `newDocument()`, and `openDocument()` methods.  

The advantage of using the Factory pattern in conjunction with the interfaces is that it provides a way to create objects without having to know the specific class or implementation details of those objects.

In the example, the `MyApplication` class implements the `Application` abstract class, which defines the `createDocument()` method that returns a `Document` object. However, the implementation of the `Document` abstract class is hidden from the `MyApplication` class, and instead, the `createDocument()` method relies on a concrete factory class to create the `Document` object.  

By using a factory to create objects, the code becomes more flexible and extensible. If we need to add a new type of `Document`, we can create a new class that implements the `Document` interface and a new factory class that creates instances of the new `Document` class. We don't have to modify the `MyApplication` class or any other parts of the code that rely on the `Document` interface, making the code easier to maintain and modify.

&nbsp;

When to use:  
Where you have a class that needs to create objects, but you don't want to tie that class to a specific object or class.  
By using a Factory Method, you can allow subclasses to decide which class to instantiate, without requiring the parent class to know the specific details of how each object is created.

From the example, this design allows new document types to be added in the future by creating new subclasses of `Application` and overriding the `createDocument()` method, without modifying the existing `Application class`.
