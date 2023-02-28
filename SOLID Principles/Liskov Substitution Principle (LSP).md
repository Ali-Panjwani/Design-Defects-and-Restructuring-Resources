Definition:  
Subtypes must be substitutable for their base types. In other words, if a class A is a subtype of class B, then objects of class A should be able to be used wherever objects of class B are expected.
  
Example:  
Suppose we have a class hierarchy for animals, where the base class is "Animal", and there are subclasses like "Dog" and "Cat". By following the LSP, we could replace a "Dog" object with an "Animal" object, and the system should still work correctly.  

Code:  
```
public class Animal {
    public void makeSound() {
        System.out.println("Generic animal sound");
    }
}

public class Dog extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Bark!");
    }
}

public class Cat extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Meow!");
    }
}
```
