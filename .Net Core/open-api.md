# Open API

**Open API** also known as Swagger is a popular tool for developing and testing APIs.

**OpenAPI** is a format for describing restful APIs, but it isn't quite a schema like HAL or Ion.

Think of **OpenAPI** as introspection or reflection for your API. You can describe your API using the language agnostic OpenAPI Spec and then give this description to others to help them understand how to interact with your API.

This API description lives in a file called **swagger.json**.

You can build a **swagger.json** file by hand or you can generate it automatically. 

**Swagger.json** can be processed to automatically create a strongly typed client for your API or to generate API tests.

Swagger.json also enables a web tool called Swagger UI which allows a human to browse to your API definition and documentation and interact with the API in real time.