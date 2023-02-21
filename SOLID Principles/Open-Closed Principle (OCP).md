Definition:
Software entities (classes, modules, functions, etc) should be open to extension and closed for modification. This means that you should be able to add new functionality to a system without changing existing code.

Example:
Suppose we have a shape class hierarchy, and we want to add a new shape like Rectangle or Circle. We would create a new class that extends the shape class, rather than modifying the shape class itself.
  
Code:  

```
public abstract class Shape {
	public abstract double area();
}

public class Rectangle extends Shape {
	private double width;
	private double height;
	
	public Rectangle(double width, double height) {
		this.width = width;
		this.height = height;
	}

	@Override
	public double area() {
		return width * height;
	}
}

public class Circle extends Shape {
	private double radius;

	public Circle(double radius) {
		this.radius = radius;
	}

	@Override
	public double area() {
		return Math.PI * radius * radius;
	}
}
```
  
Advantages:
- Flexibility: Easily extended with new functionality, without breaking the existing code makes it flexible.
- Maintainability: It is maintainable as code is not modified with new functionality.
- Reusability: Reusable code modules that can be used in multiple context.
- Testability: Easier to test, due to modules in isolation.
- Scalability: It allows scalability as new functionality can be added without modifying existing code.
  
Disadvantages:
- Complexity: Requires additional abstractions and interfaces to achieve the desired level of modularity and flexibilty. Makes the code more difficult to understand.
- Over-engineering: Developers try to anticipate every possible way the code need to be extended in the future, can result in a bloated and convulated codebase.
- Performance: Decreases performance, especially if the codeis overly abstracted. Abstraction can add additional layers of indirection and processing.
- Compatibility: There is a possbility that the existing code may not be designed with the same level of modularity and flexbility as intended from the new code. Hence it can have compatibility issues with existing code or third-party libraries.
  
Real World Application:
- Java Collection Framework is a set of classes and interfaces that provide a framework for storing and manipulating collections of objects in Java.
- WordPress allows developers to create plugins to extend its functionality. The WordPress plugin architecture is designed to be open for extension but closed for modification.
- The Android SDK provides a set of classes and interfaces that implement the OCP, allowing developers to create new types of components and behaviours that can be extended without modifying the underlying codebase.
  
Questions:
- How to avoid Over-engineering while applying OCP ?  
Start with solving the immediate problem in the simplest way possible.  
Identify areas that will be most likely to require modification or extension in future rather then building all the components with similar mentality.  
Favour composition over inheritance as inheritance might lead to over-engineering.  
Refactor the codebase to ensure that it remains maintainable and extensible meanwhile it removes unnecessary complexity.  

- How to increase Performance using OCP ?  
Use abstraction wisely because whenever you create a layer of abstraction, there is some overhead involved in accessing the layer.  
Use encapsulation wisely, keeping the internal working of a class hidden from other classes prevents performance issues that can arose from other classes directly accessing a class's internal state.  