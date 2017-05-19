# Coding Conventions I like 
## Java project

Interfaces have the name of the abstraction while implementation will have a Default prefix in front of the name. Example:
```java
public interface DeliveryAgent {
...
}
```

```java
public class DefaultDeliveryAgent implements DeliveryAgent {
...
}
```

## The Domain
* The domain module will hold all the domain abstraction with adaptor interfaces
* The domain will always contain classes that speak the domain language. For instance the logging should have his own class that has specific methods with names that descrive what you are logging and why. As an example: 
```java
public interface GatewayLogger {
  public void logNoRecipientHasBeenDiscovered(Message message);
  public void logNumberOfDiscoveredRecipient(Message message, List<Service> recipient);
  ...
}

public class Slf4jGatewayLogger {
  private Logger logger = LoggerFactory.getLogger(Slf4jGatewayLogger.class);
  
  public void logNoRecipientHasBeenDiscovered(Message message) {
    if (!logger.isInfoEnabled()) return;
    
    logger.info("no recipient has been discovered for message {}", message); 
  }
  
  ...
}
```

# Java Exceptions
- prefer unchecked exceptions over the checked ones. 
- when an exceptional behavior happens throw the unchecked exception with all the possible debugging information
- catch all the unchecked exception where it's possible to communicate to the user an ERROR message
