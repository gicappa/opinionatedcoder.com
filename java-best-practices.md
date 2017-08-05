# Java Best Practices 

## The Domain Driven Development Lesson

### Overview
A book "Pattern of Enterprise Architecture" was issued in 2002 and the IT world changed dramatically. Before that moment the world enterprise referred to the IT was just meaning "slow and bloated but it's the only way we know to do it". Pattern of enterprise architecture started speaking about *domain drive* instead of just *data driven* an instead of enforcing a new type of *EJBs* (very popular at that time) enforced the concept of *POJO*, a buzzword to rediscover Plain Old Java Objects. 
The book has been a big source of inspiration and it put the ground for some base concepts like *Domain Model* (a pattern explained in the book), *Repository Pattern* and the antipattern of an *Anemic Domain Model* representing a layered architecture.

The Java language can offer many of the advatages people search for in spring without using spring. Spring is a good framework but has the issue to add code that is not your exactly in the heart of your project. The real advantage of spring is not the dependency injection but it's some forced good architecture decision like separating the creation and wiring of the objects from the actual usage of them. This can be achieved without spring as well with some well structured code.

## The Domain
The Domain is where the action takes place. The domain is the realm of relationships and that is why in the domain the tdd London Style (with mock objects) works better thant the chicago style. The infrastructure is more a realm of functions and side effects and that is why the chicago style works better. 

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

## Coding for interfaces

Always Code for interfaces. Always rely on abstractions.Interfaces have the name of the abstraction while implementation will have a Default prefix in front of the name. Example:
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


## Application

This is where object are created and connected. 

## Infrastructure

# Java Exceptions
- prefer unchecked exceptions over the checked ones. 
- when an exceptional behavior happens throw the unchecked exception with all the possible debugging information
- catch all the unchecked exception where it's possible to communicate to the user an ERROR message. Typically the catching of instances of runtime exception can be done at 'main partition' level, in the application module.

## Runtime Classloading

Runtime classloading can be used to avoid direct dependencies from application and domain modules to the infrastructure details. The domain will used their own interface to for instance make a REST call but the implementation will be taken from a class that has no direct import anywhere in the application/domain code and will be fully substitutable without any issue with another in acordance with LSP. 
