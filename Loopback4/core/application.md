#### [Back](./README.md)

# Application

In LoopBack 4, the Application class is the central class for setting up all of your module’s components, controllers, servers and bindings. The Application class extends Context and provides the controls for starting and stopping itself and its associated servers.

When using LoopBack 4, we strongly encourage you to create your own subclass of Application to better organize your configuration and setup.

## Application Class
Application is a container for various type of artifacts, such as components, server, controller, repositories, datasources, connectors and models.

**Signature**
```typescript
export declare class Application extends Context implements LifeCycleObserver 
```

### Methods
1. **init()**
2. **Start()**
3. **Stop()**
4. **onStart(fn)**
5. **onStop(fn)**
 