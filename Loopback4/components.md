#### [Back](./README.md)

# Components of Loopback4

## Models
A model describes business domain objects and defines a list of properties with name, type, and other constraints.

Models are used for data exchange on the wire or between different systems.

### Building a Model
```bash
lb4 model
```

## Datasources
Datasources are LoopBack’s way of connecting to various sources of data, such as databases, APIs, message queues and more. A DataSource in LoopBack 4 is a named configuration for a Connector instance that represents data in an external system. The Connector is used by legacy-juggler-bridge to power LoopBack 4 Repositories for Data operations.

In LoopBack 4, datasources can be represented as strongly-typed objects and freely made available for injection throughout the application. Typically, in LoopBack 4, datasources are used in conjunction with Repositories to provide access to data.

```bash
lb4 datasource
```

## Repositories
The repository pattern is one of the more fundamental differences between LoopBack 3 and 4. In LoopBack 3, you would use the model class definitions themselves to perform CRUD operations. In LoopBack 4, the layer responsible for this has been separated from the definition of the model itself, into the repository layer.

A Repository represents a specialized Service interface that provides strong-typed data access (for example, CRUD) operations of a domain model against the underlying database or service.

```bash
lb4 repositories
```

The src/repositories/index.ts file makes exporting artifacts central and also easier to import.

The newly created todo.repository.ts class has the necessary connections that are needed to perform CRUD operations.

## Controllers
In LoopBack 4, controllers handle the request-response lifecycle for your API. Each function on a controller can be addressed individually to handle an incoming request (like a POST request to /todos), to perform business logic, and to return a response.

Controller is a class that implements operations defined by application’s API. It implements an application’s business logic and acts as a bridge between the HTTP/REST API and domain/database models.

In this respect, controllers are the regions in which most of your business logic will live!

```bash
lb4 controller
```

Let’s review the TodoController located in src/controllers/todo.controller.ts. The @repository decorator will retrieve and inject an instance of the TodoRepository whenever an inbound request is being handled. The lifecycle of controller objects is per-request, which means that a new controller instance is created for each request. As a result, we want to inject our TodoRepository since the creation of these instances is more complex and expensive than making new controller instances.

There are two new decorators to provide LoopBack with metadata about the route, verb and the format of the incoming request body:

* **@post('/todos')** creates metadata for @loopback/rest so that it can redirect requests to this function when the path and verb match.

* **@requestBody()** associates the OpenAPI schema for a Todo with the body of the request so that LoopBack can validate the format of an incoming request.

* Routes like **@get('/todos/{id}')** can be paired with the @param.path decorators to inject those values at request time into the handler function.

* LoopBack’s **@param** decorator also contains a namespace full of other “subdecorators” like @param.path, @param.query, and @param.header that allow specification of metadata for those parts of a REST request.

* LoopBack’s **@param.path** and **@param.query** also provide subdecorators for specifying the type of certain value primitives, such as @param.path.number('id').

## Sequence

A Sequence is a series of steps to control how a specific type of Server responds to incoming requests. Each types of servers, such as RestServer, GraphQLServer, GRPCServer, and WebSocketServer, will have its own flavor of sequence. The sequence represents the pipeline for inbound connections.

The contract of a Sequence is simple: it must produce a response for a request. The signature will vary by server types.

Each server type has a default sequence. It’s also possible to create your own Sequence to have full control over how your Server instances handle requests and responses.


* ### Middleware-based Sequence
* ### Action based Sequence

When a LoopBack application is scaffolded using lb4 app command, a MySequence class is generated in src/sequence.ts.

```typescript
import {MiddlewareSequence} from '@loopback/rest';

export class MySequence extends MiddlewareSequence {}
```

MySequence is then used by the RestApplication in src/application.ts
```typescript
import {BootMixin} from '@loopback/boot';
import {ApplicationConfig} from '@loopback/core';
import {RepositoryMixin} from '@loopback/repository';
import {RestApplication} from '@loopback/rest';
import {ServiceMixin} from '@loopback/service-proxy';
import {MySequence} from './sequence';

export {ApplicationConfig};

export class TodoListApplication extends BootMixin(
  ServiceMixin(RepositoryMixin(RestApplication)),
) {
  constructor(options: ApplicationConfig = {}) {
    super(options);
    // Set up the custom sequence
    this.sequence(MySequence);
    // ...
  }
}
```