Definition:
A class should have only one reason to change. In other words, a class should have only one responsibility.

Example:
If a class handles logging should only be responsible for logging and not for any other functionality, such as handling user authentication or database operations.
  
Advantages:
- The code becomes easier to maintain and modify.
- Less risk of introducing bugs or errors when making changes.
- Makes it easier to test each module in isolation.
- Allows re-using the code in other parts of the application.
- Makes the design more modular and extensible.
- This approach allows for greater scalability, flexibility, and resilience in distributed systems.
  
Disadvantages:
- Dividing the system into multiple components can lead to a more complex system architecture.
- Increases development time as more components require more time in planning, designing and testing.
- Dividing the system into many smaller components can lead to code duplication, which increases the overall size of codebase.
- Due to Modular design, components may need to communicate frequently with each other, which increases the communication overhead.
  
Real World Application:
- SRP is used in the design of the Apache HTTP Server. It seperates the responsibilities of the server into seperate modules or components, such as HTTP Protocol handling, authentication and logging. Each module has a single responsibiltity, and if a change needs to be made to one of the modules, it can be done without affecting the others.
- Microservice Architectures, where each service is responsible for a single business capability or functionality, also uses SRP. By applying SRP, each microservice has a clearly defined responsibilty, and changes to one service can be made without affecting the others.

Code:  
// The "Logger" class represents a logging utility that writes log messages to a file at the specified "filePath".
```
public class Logger {

	private String filePath;
	
	public Logger(String filePath) { //Constructor
		this.filePath = filePath;
	}

	public void Log(String message) {
		try {
			BufferedWriter writer = new BufferedWriter(new FileWriter(filePath,true)); // Indicates that the message should be appended to the end of file
			writer.write(message, '\n'); // Writing the message
			writer.close;
		} catch(IOException e) {
			e.PrintStackTrace();
		}
	}
}
```

Questions:
- How does SRP makes a System more Scalable ?  
Scalability refers to a system's ability to handle increasing amounts of data, traffic, or workload with sacrificing performance or availability.
This principle helps to make a system more scalable by promoting a modular, component-based design and seperation of concerns. Modular design allows for the system to be distributed across multiple nodes or servers. Each module can be deployed on a seperate server or cluster.
This approach can help to improve the system's performance and availability, as more resources can be added as needed to handle increasing demand.

- How does SRP adds more resilience to the distributed systems ?  
It can contribute to the resilience of distributed systems by helping to isolate faults and failures to specific components or modules.
Distributed systems are spread across multiple nodes or servers. By following SRP, the responsibilities of each module are clearly defined, and each module has a well-defined interface with the others. It makes it easier to isolate problems and troubleshoot issues when they arise.
It also contributes to resilience of distributed systems by enabling the use of redundancy and failover mechanisms. It becomes easier to replicate critical components across multiple servers or nodes. This approach can improve the system's availability and ensure that the system remains operational even if one or more components fail.

- How does SRP supports flexibility ?  
Flexibility refers to the ability of a system to adapt to changing requirements and conditions.
Modular, component-based design can also improve code reuse, which can lead to more efficient development and maintenance.
When the system is modular, developers can build new features or components on top of existing one.
