Definiton:  
The Startegy Pattern is a behavioral design pattern that lets an object change its behavior by choosing from a set of interchangeable algorithms known as strategies. The strategies are encapsulated in a group of interchangeable objects, allowing them to be easily swapped at runtime without modifying the context using them.  

Futher Explaining the Defintion:
- Interchangeable Algorithms: A set of different ways to solve the same problem. E.g. We have a list of Numbers and we need to sort them. Sorting algorithms suc as bubble sort, selection sort, and quicksort are interchangeable algorithms that can be encapsulated as strategies within a group of objects. By dynamically selecting the best strategy at runtime based on factors such as list size, a program can adapt to different scenarios without requiring to modify the code.
