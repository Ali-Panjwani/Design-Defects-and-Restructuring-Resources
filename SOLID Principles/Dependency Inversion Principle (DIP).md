Definition:
High-level modules should not depend on low-level modules. Both should depend on abstractions. Abstractions should not depend on details. Details should depend on abstractions. This means that you should depend on abstractions (interfaces) instead of concrete implementations.  

Example:  
Suppose we have a class that needs to access a database. By following the DIP, we would create an interface for the database operations, and the class would depend on the interface instead of the specific database implementation. This way, we could easily switch to a different database implementation without affecting the class.  

Code:  
```
public interface Database {
    void save(String data);
    String load();
}

public class DatabaseImpl implements Database {
    @Override
    public void save(String data) {
        // Save data to a file or database
    }
    
    @Override
    public String load() {
        // Load data from a file or database
        return "";
    }
}

public class SomeClass {
    private Database database;
    
    public SomeClass(Database database) {
        this.database = database;
    }
    
    public void doSomething() {
        String data = database.load();
        // Do something with the data
        database.save(data);
    }
}
```
