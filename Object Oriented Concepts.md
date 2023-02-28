- Some key words to Understand:  

1. Association: A relationship among two or more objects where they interact with each other to perform an operation.  


2. Composition: A relationship between two or more objects where one object is composed of one or more other objects.  

3. Aggregation: A relationship between two or more objects where one object is a container for one or more other objects.  

4. Extension (Inheritance): A relationship between two or more classes where one class inherits the properties and methods of another class.  

![Diagrams](https://1.bp.blogspot.com/-VL_9cjhwEE4/UvJN__IvaBI/AAAAAAAABCc/IkDmShgM-Yc/s1600/Association,+Composition+UML.JPG)

&nbsp;

- Object Oriented Design Rules:  

1. Program to an interface, not an implementation  
~ Don’t declare variables to be instances of particular concrete class.  
~ Abstract the process of object creation.  
  
2. Favour object composition over class inheritance.  
Inheritance lets a subclass inherit from its superclass, but can cause issues like tight coupling and maintenance problems. \
Object composition, on the other hand, creates a new class by combining objects of other classes, leading to more flexible and modular code, as it allows objects to be easily replaced or modified without affecting other parts of the code. \
~ Reusing by inheritance in white-box re-use -> it exposes the implementation details of the superclass to the subclass, and changes to the superclass can affect the behavior of the subclass. \
~ Reusing composition for black-box re-use -> the implementation details of the objects being composed are hidden from the new class, and changes to the composed objects do not affect the new class, as long as the interface remains unchanged.
