# Load balancing
## HAProxy solution

* multiple A records in DNS 
* multiple HAProxy in a crossed configuration (active and passive)
* we application, databases...

## Facebook.com


* Dynamic Requests 
  * Newsfeed
  * Likes 
  * Messaging 
  * Status Updates
* Static Requests (CDN)
  * Photos
  * Videos
  * Javascript/CSS
  
Egress: byte outgoing / Ingress: byte ingoing

They support: HTTP, SPDY, MQTT

### Serving Dynamic Facebook requests

10% IPv6
100 TB/s throuh all datacenters

They have a L7 Load Balancer called proxygen (https://code.facebook.com/posts/1503205539947302/, https://code.facebook.com/projects/676603015770415/)
They use zookeeper as a service discovery mechanysm

In front of L7LB they put a L4LB with ipvs (http://www.linuxvirtualserver.org/software/ipvs.html)

In front of this they put an appliance called ECMP (Equal Cost Multi Pathing)

### L4/L7 Load Balancing 
### Edge pop and reducing Latencies
### Global DNS Load Balancing

