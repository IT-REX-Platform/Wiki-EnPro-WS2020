# Reverse Proxy

## Reverse proxies
* Nginx ("engine-ex")
* HAProxy

## Purpose
A reverse proxy is a server between clients and backend server/s. It accepts requests from browsers and mobile apps and retrieves resources from servers for clients. So when a client sends a request to a server, he adresses the reverse proxy, which acts as a "public face" for backend.

## Example (Ngnix)
![Reverse_Proxy](./Images/Reverse_Proxy.png)

## Pros
* SSL termination: encryption of incoming client requests and decryption of outgoing server responses. A reverse proxy can provide SSL encryption for a number of web servers, which won't need separate SSL Server Certificates. This also frees up resources on those servers.
* Caching: reverse proxy stores a copy of server's response before returning it. This copy is used if a client makes the same request, resulting in backend server load reduction.
* Compression: reverse proxy can compress server responses to reduce bandwidth use which also reduces load time.
* Scalability: clients only see reverse proxy's IP address, leaving developers free to change backend infrastructure configuration.
* Load balancing: if multiple backend servers are deployed, the workload can be distributed evenly. Down servers are detected and requests are diverted to other servers. Security: additional layer of defence.

## Cons
* Single point of failure.
* If compromised by a malicious party a reverse proxy can log all sensitive information going through it or inject malware.

## Further reading
| Topic | Link |
| :--- | :--- |
| Reverse proxies | https://www.nginx.com/resources/glossary/reverse-proxy-vs-load-balancer <br> https://en.wikipedia.org/wiki/Proxy_server#Reverse_proxies <br> https://en.wikipedia.org/wiki/Reverse_proxy |
| HAProxy | https://en.wikipedia.org/wiki/HAProxy <br> https://www.haproxy.com |
| Nginx | https://en.wikipedia.org/wiki/Nginx <br> https://www.nginx.com |

