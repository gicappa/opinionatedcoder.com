# Keypoints
Service can be expressed so that a service starts after another one, but microservices 
are expected to be resilient so that if a service dies or is moved the connected services should
retry the connection for a certain amount of time. This is something that is not expected 
in a silo/monolyth application
