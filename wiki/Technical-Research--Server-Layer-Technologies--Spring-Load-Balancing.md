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


# Spring Cloud LoadBalancer

Spring Cloud LoadBalancer provides an abstraction for other load client side balancing. It does essentially the same thing that Ribbon does but can use different implementations. In contrast to Ribbon it is still in active development. This makes it a better choice than the Netflix stuff (except maybe Eureka).

# Ngnix