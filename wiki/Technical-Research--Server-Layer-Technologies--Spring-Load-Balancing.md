# Eureka

Eureka is a Service Registry. It's part of the Netflixs OSS. It can used for client side load balancing and is thus a viable tool for our purposes. Services that register with it send a heartbeat every few seconds and to indicate that they are still running. Netflix also provides a library called Ribbon. Ribbon implements client side load balancing with different registries (e.g. Eureka, ZooKeeper, ...). Ribbon gets all available instances of a service from the registry and decides for itself to which service the request goes to. The choosing algorithm can be specified. All of Netflixs Spring libraries are in maintenance mode except Eureka.

# Spring Cloud LoadBalancer

Spring Cloud LoadBalancer provides an abstraction for other load client side balancing. It does essentially the same thing that Ribbon does but can use different implementations. In contrast to Ribbon it is still in active development. This makes it a better choice than the Netflix stuff (except maybe Eureka).

# Ngnix