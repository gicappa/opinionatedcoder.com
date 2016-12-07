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

## The domain module will hold all the domain abstraction with adaptor interfaces

# Java Exceptions
- prefer unchecked exceptions over the checked ones. 
- when an exceptional behavior happens throw the unchecked exception with all the possible debugging information
- catch all the unchecked exception where it's possible to communicate to the user an ERROR message
