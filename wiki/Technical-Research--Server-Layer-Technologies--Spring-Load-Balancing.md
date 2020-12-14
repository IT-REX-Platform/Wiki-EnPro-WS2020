# Eureka

Eureka is a Service Registry. It's part of the Netflixs OSS. It can used for client side load balancing and is thus a viable tool for our purposes. Services that register with it send a heartbeat every few seconds (time intervall can be configured) to indicate that they are still running. Eureka can be made more resilient by running multiple instances and registering them with each other. Netflix also provides a library called Ribbon. Ribbon implements client side load balancing with different registries (e.g. Eureka, ZooKeeper, ...). Ribbon gets all available instances of a service from the registry and decides for itself to which service the request goes to. The choosing algorithm can be specified. If server side load balancing is prefered one can use Zuul to achieve that. 

- spring-cloud-netflix-archaius
- spring-cloud-netflix-hystrix-contract
- spring-cloud-netflix-hystrix-dashboard
- spring-cloud-netflix-hystrix-stream
- spring-cloud-netflix-hystrix
- spring-cloud-netflix-ribbon
- spring-cloud-netflix-turbine-stream
- spring-cloud-netflix-turbine
- spring-cloud-netflix-zuul

https://cloud.spring.io/spring-cloud-netflix/reference/html/

https://m.heise.de/developer/artikel/Eureka-Microservice-Registry-mit-Spring-Cloud-2848238.html?seite=all

https://www.baeldung.com/zuul-load-balancing

https://www.baeldung.com/spring-cloud-netflix-eureka


# Spring Cloud

Spring Cloud provides tools for developers to quickly build common patterns in deistributed systems. Spring Cloud offers tools to achieve Load Balancing. This is achieved by an abstraction layer that can take multiple different implementations, including but not limited to the Netflix OSS. It does offer alternatives to ribbon but there seems to be no alternative to Zuul. This means one has to stay with Zuul or use an external service. Despite that you should use the provided abstraction layer and all the utilities provided by Spring Cloud because they can still use the Netflix OS components.

https://spring.io/projects/spring-cloud

# Ngnix

Nginx is a web server that provides 
- A reverse proxy with caching
- IPv6
- Load balancing
- FastCGI with caching
- WebSockets
- Handling of static files, indexfiles and automatic indexing
- TLS/SSL with SNI

Nginx does not have a service registry. This means you need to have a custom sloution for that. One possible solution is to use [Consul Template to dynamically reconfigure configuration files](https://www.airpair.com/scalable-architecture-with-docker-consul-and-nginx). This task can also be done by a container orchestrator like Kubernetes. The greatest benefit of using Nginx (or any other server side load balancing solution) is that it requires less communication before the actual request starts than client side load balancing, which requires fetching the list of possible endpoints before the request can be made. 

https://kinsta.com/de/wissensdatenbank/was-ist-nginx/
https://www.nginx.com/blog/service-discovery-in-a-microservices-architecture/