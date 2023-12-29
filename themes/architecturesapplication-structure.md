# Application Structure
```
app-main
app-domain
app-cache
app-mq
  \
   src
   test
   resources
   test-resources
   pom.xml
app-ds
app-rest-client
app-rest-server
app-xml
app-security
adapter-mq-rabbitmq
adapter-ds-consul
adapter-ds-zookeeper

scripts
initialization
config
infrastructure
  \
   database
pom.xml
```

It should be clearly stated how and where the initialization of the application is happening.
The same applies to the configuration
