# Configurations

The opinionated choice for supporting java properties is owner from aeonbits. It's a really nice lib that just does one thing well. The idea is to use it in conjuction to the system properties in order to have the chance to modify option using Java system properties expressed at command line and to override some settings for testing purposes.

```java
GatewayConfig config = ConfigFactory.create(GatewayConfig.class, System.getProperties());
```
