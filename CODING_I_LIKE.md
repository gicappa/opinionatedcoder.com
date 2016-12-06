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
