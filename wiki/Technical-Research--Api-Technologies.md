# API Technologies

## REST vs GraphQL


In order to handle the http communication between services, GraphQL was evaluated and compared to REST apis - the most common approach for microservice-based applications.

It turns out that [GraphQL](https://medium.com/tech-tajawal/backend-for-frontend-using-graphql-under-microservices-5b63bbfcd7d9) can be used as an alternative for REST because of less network traffic and higher scalability.
The main differences between a REST-based Api and a GraphQL Api are listed in the following:


**Data Acquisition:** REST lacks scalability and GraphQL can be accessed on demand. The payload can be extended when the GraphQL API is called. <br>
**API calls:** REST’s operation for each resource is an endpoint, and GraphQL only needs a single endpoint, but the post body is not the same. <br>
**Complex data requests:** REST requires multiple calls for nested complex data, GraphQL calls once, reducing network overhead. <br>
**Error code processing:** REST can accurately return HTTP error code, GraphQL returns 200 uniformly, and wraps error information. <br>
**Version number:** REST is implemented via v1/v2, and GraphQL is implemented through the Schema extension. <br>

The first idea was to evaluate if a GraphQL Api could be used between the Backend and Frontend.
This would enable a uniform way to gather information about the backend by connecting to one single endpoint.
With the help of GraphQL, queries could be very flexible so that the consuming side only gathers the relevant information. This could reduce traffic and be more efficient compared to a REST-based approach.

On the other hand a REST api would be simpler to implement and easier to understand, because the technology is well-known among the students.

Finally, we decided on using REST apis for all http communication. The main reason was that the expected amount of data per request is not high enough to justify a GraphQL Api.
In addition, it is more complex to implement and each student would need to spend time in order to understand the schemas and queries in GraphQL.