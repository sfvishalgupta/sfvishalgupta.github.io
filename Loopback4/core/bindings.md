#### [Back](./README.md)

# Bindings

## What is Binding?
Binding represents items within a Context instance. A binding connects its value to a unique key as the address to access the entry in a context.

### Attributes of a binding
A binding typically has the following attributes:

* **key**: Each binding has a key to uniquely identify itself within the context
* **scope**: The scope controls how the binding value is created and cached within the context
* **tags**: Tags are names or name/value pairs to describe or annotate a binding
* **value**: Each binding must be configured with a type of value provider so that it can be resolved to a constant or calculated value

## Binding Type

### to(): A Constant Value
If binding is always resolved to a fixed value, we can bind it to a constant, which can be a string, a function, an object, an array, or any other types.
```typescript
binding.to('my-value');
```

### toDynamicValue(): A Factory function to return a value 
Sometimes the value needs to be dynamically calculated, such as the current time or a value fetched from a remote service or database.
```typescript
binding.toDynamicValue(() => 'my-value');
binding.toDynamicValue(() => new Date());
binding.toDynamicValue(() => Promise.resolve('my-value'));
```

The factory function can receive extra information about the context, binding, and resolution options.
```typescript
import {ValueFactory} from '@loopback/core';

// The factory function now have access extra metadata about the resolution
const factory: ValueFactory<string> = resolutionCtx => {
  return `Hello, ${resolutionCtx.context.name}#${
    resolutionCtx.binding.key
  } ${resolutionCtx.options.session?.getBindingPath()}`;
};
const b = ctx.bind('msg').toDynamicValue(factory);
```

Object destructuring can be used to further simplify a value factory function that needs to access context, binding, or options.
```typescript
const factory: ValueFactory<string> = ({context, binding, options}) => {
  return `Hello, ${context.name}#${
    binding.key
  } ${options.session?.getBindingPath()}`;
};
```

An advanced form of value factory is a class that has a static value method that allows parameter injection.
```typescript
import {inject} from '@loopback/core';

class GreetingProvider {
  static value(@inject('user') user: string) {
    return `Hello, ${user}`;
  }
}

const b = ctx.bind('msg').toDynamicValue(GreetingProvider);
```
### toClass(): A Class
The binding can represent an instance of a class, for example, a controller. A class can be used to instantiate an instance as the resolved value. Dependency injection is often leveraged for its members.

```typescript
class MyController {
  constructor(@inject('my-options') private options: MyOptions) {
    // ...
  }
}
binding.toClass(MyController);
```

### toProvider(): A Provider
A provider is a class with value() method to calculate the value from its instance. The main reason to use a provider class is to leverage dependency injection for the factory function.

```typescript
class MyValueProvider implements Provider<string> {
  constructor(@inject('my-options') private options: MyOptions) {
    // ...
  }

  value() {
    return this.options.defaultValue;
  }
}

binding.toProvider(MyValueProvider);
```
The provider class serves as the wrapper to declare dependency injections. If dependency is not needed, toDynamicValue can be used instead.

### toInjectable(): An injectable class
An injectable class is one of the following types of classes optionally decorated with @injectable.
* A class
* A provider class
* A dynamic value factory class

The toInjectable() method is a shortcut to bind such classes using toClass/toProvider/toDynamicValue respectively by introspecting the class, including the binding metadata added by @injectable.

```typescript
@injectable({scope: BindingScope.SINGLETON})
class MyController {
  constructor(@inject('my-options') private options: MyOptions) {
    // ...
  }
}

binding.toInjectable(MyController);
```

The code above is similar as follows:
```typescript
const binding = createBindingFromClass(MyController);
```


### toAlias(): A Alias
An alias is the key with optional path to resolve the value from another binding. For example, if we want to get options from RestServer for the API explorer, we can configure the apiExplorer.options to be resolved from servers.RestServer.options#apiExplorer.
```typescript
ctx.bind('servers.RestServer.options').to({apiExplorer: {path: '/explorer'}});
ctx
  .bind('apiExplorer.options')
  .toAlias('servers.RestServer.options#apiExplorer');
const apiExplorerOptions = await ctx.get('apiExplorer.options'); // => {path: '/explorer'}
```