# API Technologies

## REST vs GraphQL


A great alternative to REST is the Query Language [GraphQL](https://medium.com/tech-tajawal/backend-for-frontend-using-graphql-under-microservices-5b63bbfcd7d9) because of less network traffic and higher scalability.

_Comparison of REST and GraphQL:_ <br>
**Data Acquisition:** REST lacks scalability and GraphQL can be accessed on demand. The payload can be extended when the GraphQL API is called. <br>
**API calls:** REST’s operation for each resource is an endpoint, and GraphQL only needs a single endpoint, but the post body is not the same. <br>
**Complex data requests:** REST requires multiple calls for nested complex data, GraphQL calls once, reducing network overhead. <br>
**Error code processing:** REST can accurately return HTTP error code, GraphQL returns 200 uniformly, and wraps error information. <br>
**Version number:** REST is implemented via v1/v2, and GraphQL is implemented through the Schema extension. <br>