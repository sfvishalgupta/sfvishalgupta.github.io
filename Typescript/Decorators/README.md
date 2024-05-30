#### [Back](../README.md)

# Decorators
A Decorator is a special kind of declaration that can be attached to a **class declaration, method, accessor, property, or parameter**. Decorators use the form @expression, where expression must evaluate to a function that will be called at runtime with information about the decorated declaration.

## How to use decorators:
To enable experimental support for decorators, you must enable the experimentalDecorators compiler option either on the command line using tsc --target ES5 --experimentalDecoratorsor in your tsconfig.json:

```json
{
  "compilerOptions": {
    "target": "ES5",
    "experimentalDecorators": true
  }
}
```

Consider a user class with a method greet

```typescript
class User {
  constructor(private name: string, private age: number) {}

  greet() {
    console.log(`Hello, my name is ${this.name}.`);
  }

  printAge() {
    console.log(`I am ${this.age} years old`);
  }
}

const user = new User("Ron", 25);
user.greet();
user.printAge();


Output: 
Hello, my name is Ron.
I am 25 years old
```

Now we want to log when each function execution starts and ends:

```typescript
class User {
  constructor(private name: string, private age: number) {}

  greet() {
    console.log('start: greet')
    console.log(`Hello, my name is ${this.name}.`);
    console.log('end: greet')
  }

  printAge() {
    console.log('start: printAge')
    console.log(`I am ${this.age} years old`);
    console.log('end: printAge')
  }
}

const user = new User("Ron", 25);
user.greet();
user.printAge();


Output: 
start: greet
Hello, my name is Ron.
end: greet
start: printAge
I am 25 years old
end: printAge
```

**Now think about it, Can we reuse this logic of logging function execution start and end? Yes, we can create a wrapper function that logs the start and end of the wrapped function. That’s what decorators do for us in a neat and clean way. Let’s see how**

It’s super easy to create a decorator: Just create a function called **logger** :

```typescript
function logger(originalMethod: any, _context: any) {
  function replacementMethod(this: any, ...args: any[]) {
    console.log("start:", originalMethod.name);
    const result = originalMethod.call(this, ...args);
    console.log("end:", originalMethod.name);
    return result;
  }

  return replacementMethod;
}
```
That’s it. We are ready to decorate the methods. Let’s use decorators in the above example:
```typescript
class User {
  constructor(private name: string, private age: number) {}

  @logger
  greet() {
    console.log(`Hello, my name is ${this.name}.`);
  }

  @logger
  printAge() {
    console.log(`I am ${this.age} years old`);
  }
}

const user = new User("Ron", 25);
user.greet();
user.printAge();



Output: 
start: greet
Hello, my name is Ron.
end: greet
start: printAge
I am 25 years old
end: printAge
```

the following steps are performed when evaluating multiple decorators on a single declaration in TypeScript:

1. The expressions for each decorator are evaluated top-to-bottom.
2. The results are then called as functions from bottom-to-top.

## Examples
```typescript
class User {
  constructor(private name: string, private age: number) {}

  @logger2
  @logger1
  greet() {
    console.log(`Hello, my name is ${this.name}.`);
  }
}

const user = new User("Ron", 25);
user.greet();


function logger1(originalMethod: any, _context: any) {
  function replacementMethod(this: any, ...args: any[]) {
    console.log("log1");
    const result = originalMethod.call(this, ...args);
    return result;
  }

  return replacementMethod;
}

function logger2(originalMethod: any, _context: any) {
  function replacementMethod(this: any, ...args: any[]) {
    console.log("log2");
    const result = originalMethod.call(this, ...args);
    return result;
  }

  return replacementMethod;
}


Output: 
log2
log1
Hello, my name is Ron.
```

## Type of Decorators
1. ### [Class Decorators](./classDecorators.md)
2. ### [Method Decorators](./methodDecorators.md)
3. ### [Accessor Decorator](./accessorDecoratos.md)
4. ### [Property Decorator](./propertyDecorators.md)
5. ### [Parameter Decorator](./parameterDecoratos.md)

### Use Cases of Decorators
1. Logging and Debugging
2. Validation
3. Memoization
4. Authentication and Authorization
5. Dependency Injection
6. Route Handling (Web Applications)
7. Data Transformation
8. Caching
9. Timing and Profiling
10. Logging Frameworks
11. Validation Frameworks
12. Database Mapping
13. Property Access Control
14. Singleton Pattern
15. Custom Middleware
16. Internationalization and Localization
17. Error Handling
18. Event Handling
19. Type Checking and Transformation
20. Custom Annotations


