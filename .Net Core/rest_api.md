# REST API

using HTTP methods like GET and POST or your API supports CRUD operations doesn't make your API RESTful. That just means that you're using HTTP. And just because an API returns JSON, doesn't make it RESTful either. There are plenty of non-REST APIs that return JSON.

**REST** is is all about modelling your API around resources and allowing clients to perform operations on those resources. In the context of REST, a resource is any object in your API's design domain. Things like documents, users, orders, reservations, and tasks. In many cases a resource will correlate exactly with a row in a table or an object in the database but that's not always the case. So instead of having API endpoints that are verbs or represent actions you can take in the system, the endpoints in a RESTful API represent resources or collections of those resources. In addition, relationships between data are represented by relationships between the resources in your API.

REST vs. RPC

In a **REST API**, calling an endpoint acts on a resource using an HTTP method as the verb. For example, sending a GET request to /users/123 retrieves the details of the user with that id. To update the user you might send a POST request and a request body.

An **RPC** API uses HTTP methods as well, but it is very similar to calling a function in any programming language. You call the function by name, pass some arguments or parameters, and get a response.

Both **REST** and **RPC** use HTTP methods and both styles could return XML, JSON or some other format entirely.

**REST API** is the PayPal API, which lets clients create and manipulate objects that represent payments, invoices, billing plans and so on. On the other hand, an **RPC** style might fit your API better if your API is action driven; for example, you need send an event or command to a server or remote device. **RPC API's** are good when you need to design a strict set of ways the client can interact with the server. A popular example of an RPC API is the Slack API, which lets clients preform actions like joining a channel and sending a message by sending function calls to the API.
