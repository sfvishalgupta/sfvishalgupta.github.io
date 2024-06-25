#### [Back](./README.md)

# Components

A Component makes it easy for independent developers to contribute additional features to LoopBack. Components serve as a vehicle to group extension contributions such as Context Bindings and various artifacts to allow easier extensibility of your Application.

A typical LoopBack component is an npm package exporting a Component class which can be added to your application.

Apart from its own properties, Component class can have the following properties:
* **controllers** - An array of controller classes.
* **providers** - A map of providers to be bound to the application context.
* **classes** - A map of TypeScript classes to be bound to the application context.
* **servers** - A map of name/class pairs for servers.
* **lifeCycleObservers** - An array of life cycle observers.
* **services** - An array of service classes or providers.
* **bindings** - An array of bindings to be added to the application context. A good example of using bindings to extend the functionality of a LoopBack 4 app is contributing an additional body parser.

These properties contribute to the application to add additional features and capabilities.

## Component Life Cycle
A component will be instantiated when app.component() is called. A component class can use its constructor and properties to contribute bindings to the hosting application. Dependency injection is supported, for example, to access the hosting application. But you have to make sure that all dependencies can be resolved synchronously when app.component() is invoked.

```typescript
import {
  Component,
  LifeCycleObserver,
  CoreBindings,
  inject,
} from '@loopback/core';

export class MyComponent implements Component, LifeCycleObserver {
  status = 'not-initialized';
  initialized = false;

  // Contribute bindings via properties
  controllers = [];
  bindings = [];

  constructor(@inject(CoreBindings.APPLICATION_INSTANCE) private app) {
    // Contribute bindings via constructor
    this.app.bind('foo').to('bar');
  }
}
```

In some cases, a component may need to contribute bindings asynchronously. It should then use the init method.
```typescript
export class MyComponent implements Component, LifeCycleObserver {
  // ...

  async init() {
    // Contribute bindings via `init`
    const val = await readFromConfig();
    this.app.bind('abc').to(val);

    this.status = 'initialized';
    this.initialized = true;
  }

  async start() {
    this.status = 'started';
  }

  async stop() {
    this.status = 'stopped';
  }
}
```

## Using Components
Components can be added to your application using the **app.component()** method.

The following is an example of installing and using a component.

Install the following dependencies:
```bash
npm install --save @loopback/authentication
```

To load the component in your application:
```typescript
import {RestApplication} from '@loopback/rest';
import {AuthenticationComponent} from '@loopback/authentication';

const app = new RestApplication();
// Add component to Application, which provides bindings used to resolve
// authenticated requests in a Sequence.
app.component(AuthenticationComponent);
```

## Official components
Here is a list of components officially created and maintained by the LoopBack team.


## Core Components
These components implement the primary LoopBack capabilities.

* **@loopback/authentication** - A LoopBack component for authentication support
* **@loopback/authorization** - A LoopBack component for authorization support
* **@loopback/boot** - A collection of Booters for LoopBack 4 Applications
* **@loopback/booter-lb3app** - A booter component for LoopBack 3 applications to expose their REST API via LoopBack 4
* **@loopback/rest** - Expose controllers as REST endpoints and route REST API requests to controller methods
* **@loopback/rest-crud** - REST API controller implementing default CRUD semantics
* **@loopback/rest-explorer** - LoopBack’s API Explorer

## Extensions
These components add additional capabilities to LoopBack.

* **@loopback/apiconnect** - An extension for integrating with IBM API Connect
* **@loopback/authentication-jwt** - Extension for JWT authentication
* **@loopback/authentication-passport** - A package creating adapters between the passport module and @loopback/authentication
* **@loopback/context-explorer** - Visualize context hierarchy, bindings, configurations, and dependencies
* **@loopback/cron** - Schedule tasks using cron-like syntax
* **@loopback/health** - An extension exposes health check related endpoints with LoopBack 4
* **@loopback/logging** - An extension exposes logging for Winston and Fluentd with LoopBack 4
* **@loopback/metrics** - An extension exposes metrics for Prometheus with LoopBack 4
* **@loopback/pooling** - Resource pooling service for LoopBack 4
* **@loopback/typeorm** - Adds support for TypeORM in LoopBack
* **@loopback/sequelize** - Adds support for Sequelize in LoopBack

