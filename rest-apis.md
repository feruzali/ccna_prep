---
description: Day 61
---

# REST APIs

### HTTP

**CRUD** (Create, Read, Update, Delete) refers to the operations performed using REST APIs. **Create** operations are used to create new variables and set their initial values. **Read** operations are used to retrieve the value of a variable. **Update** operations are used to change the value of a variable. **Delete** operations are used to delete variables.

**HTTP** (HyperText Transfer Protocol) uses verbs (methods) that map to these CRUD operations. REST APIs typically use HTTP.

<figure><img src=".gitbook/assets/image (171).png" alt="HTTP verbs" width="563"><figcaption></figcaption></figure>

When an HTTP client sends a request to an HTTP server, the HTTP header includes an HTTP verb and a **URI** (Uniform Resource Identifier) indicating the resource it is trying to access.

<figure><img src=".gitbook/assets/image (172).png" alt="URI example" width="563"><figcaption></figcaption></figure>

The HTTP request can include additional headers which pass additional information to the server, e.g. an `Accept` header informs the server about the type of data that can be sent to the client.

The server's response includes a status code indicating the request succeeded or failed and some other details. The first digit indicates the class of the response:

* 1 (information) - the request was received, continuing the process
* 2 (successful) - the request was successfully received, understood, and accepted
* 3 (redirection) - further action needs to be taken to complete the request
* 4 (client error) - the request contains bad syntax or cannot be fulfilled
* 5 (server error) - the server failed to fulfil a valid request

### REST

**REST** (Representation State Transfer) APIs are also known as **REST-based API**s or **RESTful API**s. REST is not a specific API. Instead, it describes a set of rules about how the API should work. The six constraints of RESTful architecture:

* uniform interface
* client-server - they can both change and evolve independently of each other. When the client or the server application changes, the interface between them must not break.&#x20;
* stateless - each API exchange is a separate event, independent of all past exchanges between the client and server. The server doesn't store information about previous requests from the client to determine how it should respond to new requests. If authentication is required, the client must authenticate with the server for each request it makes.
* cacheable or non-cacheable - REST APIs must support caching of data but not all resources have to be cacheable. **Caching** refers to storing data for future use.&#x20;
* layered system
* code-on-demand (optional)

{% file src=".gitbook/assets/Day 61 Flashcards - REST APIs.apkg" %}
