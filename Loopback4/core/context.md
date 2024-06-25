#### [Back](./README.md)

# Context

## What is Context?
* An abstraction of all state and dependencies in your application
LoopBack uses context to manage everything

* A global registry for anything/everything in your app (all configs, state, dependencies, classes, etc)

* An inversion of control container used to inject dependencies into your code

## Why is it important?
* You can use the context as a way to give loopback more “info” so that other dependencies in your app may retrieve it. It works as a centralized place/ global built-in/in-memory storage mechanism.

* LoopBack can help “manage” your resources automatically (through Dependency Injection and decorators).

* You have full access to updated/real-time application and request state at all times.

## How to create a context?
A context can be created with an optional parent and an optional name. If the name is not provided, a unique identifier will be generated as the value. Context instances can be chained using the parent to form a hierarchy. For example, the code below creates a chain of three contexts: reqCtx -> serverCtx -> rootCtx.
```typescript
import {Context} from '@loopback/core';

const rootCtx = new Context('root-ctx'); // No parent
const serverCtx = new Context(rootCtx, 'server-ctx'); // rootCtx as the parent
const reqCtx = new Context(serverCtx); // No explicit name, a unique id will be generated
```

LoopBack’s context system allows an unlimited amount of Context instances, each of which may have a parent Context.

An application typically has three “levels” of context: application-level, server-level, and request-level.

### Application-level context (global)

* Stores all the initial and modified app states throughout the entire life of the app (while the process is alive)
* Generally configured when the application is created (though the context may be modified while running)

Here is a simple example:
```typescript
import {Application} from '@loopback/core';

// Please note `Application` extends from `Context`
const app = new Application(); // `app` is a "Context"
class MyController {}
app.controller(MyController);
```
In this case, you are using the .controller helper method to register a new controller. The important point to note is MyController is actually registered into the Application Context (app is a Context).

### Server-level context
Server-level context:
* Is a child of application-level context
* Holds configuration specific to a particular server instance

Your application will typically contain one or more server instances, each of which will have the application-level context as its parent. This means that any bindings that are defined on the application will also be available to the server(s), unless you replace these bindings on the server instance(s) directly.

For example, @loopback/rest has the RestServer class, which sets up a running HTTP/S server on a port, as well as defining routes on that server for a REST API. To set the port binding for the RestServer, you would bind the RestBindings.PORT key to a number.

We can selectively re-bind this value for certain server instances to change what port they use:
```typescript
// src/application.ts
async start() {
  // publicApi will use port 443, since it inherits this binding from the app.
  app.bind(RestBindings.PORT).to(443);
  const publicApi = await app.getServer<RestServer>('public');
  const privateApi = await app.getServer<RestServer>('private');
  // privateApi will be bound to 8080 instead.
  privateApi.bind(RestBindings.PORT).to(8080);
  await super.start();
}

```

### Request-level context (request)
Using @loopback/rest as an example, we can create custom sequences that:

* are dynamically created for each incoming server request
* extend the application level context to give you access to application-level dependencies during the request/response lifecycle
* are garbage-collected once the response is sent for memory management

```typescript
import {DefaultSequence, RestBindings, RequestContext} from '@loopback/rest';
class MySequence extends DefaultSequence {
  async handle(context: RequestContext) {
    // RequestContext provides request/response properties for convenience
    // and performance, but they are still available in the context too
    const req = await this.ctx.get(RestBindings.Http.REQUEST);
    const res = await this.ctx.get(RestBindings.Http.RESPONSE);
    this.send(res, `hello ${req.query.name}`);
  }
}
```
* this.ctx is available to your sequence
* allows you to craft your response using resources from the app in addition to the resources available to the request in real-time (right when you need it)

## Storing and retrieving items from a Context
Items in the Context are indexed via a key and bound to a BoundValue. A BindingKey is simply a string value and is used to look up whatever you store along with the key. For example:
```typescript
// app level
const app = new Application();
app.bind('hello').to('world'); // BindingKey='hello', BoundValue='world'
console.log(app.getSync<string>('hello')); // => 'world'
```

The process of registering a BoundValue into the Context is known as **binding**.

## Dependency injection
* Many configs are adding to the Context during app instantiation/boot time by you/developer.
* When things are registered, the Context provides a way to use your dependencies during runtime.

How you access these things is via low level helpers like app.getSync or the sequence class that is provided to you as shown in the example in the previous section.

However, when using classes, LoopBack provides a better way to get at stuff in the context via the @inject decorator:

```typescript
import {inject, Application} from '@loopback/core';

const app = new Application();
app.bind('defaultName').to('John');

export class HelloController {
  constructor(@inject('defaultName') private name: string) {}

  greet(name?: string) {
    return `Hello ${name || this.name}`;
  }
}
```

Notice we just use the default name as though it were available to the constructor. Context allows LoopBack to give you the necessary information at runtime even if you do not know the value when writing up the Controller. The above will print Hello John at run time.