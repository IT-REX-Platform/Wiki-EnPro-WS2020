# Best Practices for Designing HTTP APIs inspired by REST

## Preliminary 
Representational State Transfer (REST) is an architectural style for web applications. One of its properties is the design of uniform interfaces, often referred to as REST APIs or RESTful APIs. REST is no standard and no protocol, and often confused with the notion of using HTTP. However, best practices inspired by REST APIs can be commonly applied to any form of HTTP API.

## References

Main content taken from [Giessler et. al](https://www.researchgate.net/profile/Roland_Steinegger2/publication/301694429_Best_Practices_for_the_Design_of_RESTful_Web_Services/links/57231ec908ae262228a89d6f/Best-Practices-for-the-Design-of-RESTful-Web-Services.pdf). It's a good, short read. However, some strong opinions will be discussed more objectively here. 

## Best Practices

### Resources 
Resources are the core concept of referencing entities with a URI (Uniform Resource Identifiers)
* use nouns only
* use plural (e.g. ```/articels/``` instead of ```/article/```)
* implement two URIs per resource: ```/articels/``` for a collection, ```/articels/{id}``` for single entity access
* avoid unnecessary nesting of URIs (e.g. ```/editions/{ed_id}/articels/{art_id}/authors/{aut_id}/```)

### Representations and Media Types
Representations of resources are used to exchange information. Typically, lightweight media types such as JSON are used (even though JSON isn't exaclty RESTful). Best practice is to use content negotiation for clients to indicate expected media types (see [RFC7231](https://httpwg.org/specs/rfc7231.html#content.negotiation).)

Sometimes, content negotiation might be difficult to implement. Common alternative concepts are: 
* file endigs (e.g. ```/articels.json```)
* query parameters (e.g. ```/articels?format=json```)
**Weakness:** No defined media types - best practice is content negotiation.

### HTTP Methods 
HTTP Methods enable self-contained messages to invoke API-functionality. See full list of methods in [RFC7231](https://httpwg.org/specs/rfc7231.html#method.definitions). The most important ones:

| HTTP-Method | CRUD-Equivalent |
| ----------- | --------------- |
| GET | Read |
| POST | Create |
| PUT | Update |
| DELETE | Delete |

* no verbs in URIs (e.g. ```/getArticels/```)
* self-contained message semantics with HTTP Method + URI => ```[GET] /articels/```

### HTTP Status Codes and Error Handling
HTTP Status Codes enable quick, well-defined responses. Return suitable status codes with your HTTP response. See full list of status codes in [RFC7231](https://httpwg.org/specs/rfc7231.html#status.codes). The most important ones:

| Value | Description |
| ----- | ----------- |
| 200 | OK |
| 201 | Created |
| 400 | Bad Request |
| 401 | Unauthorized |
| 404 | Not Found |
| 500 | Internal Server Error |

If an error occurs, best practice is to return an additional error message/error code in the HTTP response body. 

### API Documentation

Best practice for HTTP APIs is the OpenAPI-Specification (fka Swagger): https://swagger.io/specification/ 

### API Versioning

One of the most debated topics: is versioning needed?

Best Practices (if API is versioned): 
* URI-Path (e.g. ```/v1/articels/```)
* HTTP-Header Variable

### Callback Mechanisms

For long-running tasks, there is often the implementation of callback-mechanisms (avoid HTTP-timeouts). -> has to be researched further 

### Query Parameters

[optional, best practice for complex APIs with a lot of variablity] URI query parameters may be used for the following purposes:
* filtering (e.g. ```[GET] /articels?author=mueller&date=2021-01-11```)
* sorting (e.g. ```[GET] /articels?sort=date-asc```)
* selection (e.g. ```[GET] /articels?fields=title,author,date```) 
* pagination (e.g. ```[GET] /articels?offset=0,limit=10```)

Filtering and pagination can be used to only retrieve a subset of a collection of entities. Selection is an orthogonal concept targetting to retrieve only certain attributes of the requested entities).