#### [Back](./README.md)

# Parameter Decorators
A Parameter Decorator is declared just before a parameter declaration. The parameter decorator is applied to the function for a class constructor or method declaration. A parameter decorator cannot be used in a declaration file, an overload, or in any other ambient context (such as in a declare class).

The expression for the parameter decorator will be called as a function at runtime, with the following three arguments:

1. Either the constructor function of the class for a static member, or the prototype of the class for an instance member.
2. The name of the member.
3. The ordinal index of the parameter in the function’s parameter list.

```typescript
// Parameter Decorator for Email Validation
function ValidateEmail(target: any, methodName: string, parameterIndex: number) {
  const originalMethod = target[methodName];

  target[methodName] = function (...args: any[]) {
    const paramValue = args[parameterIndex];

    // Regular expression for a simple email validation
    const emailPattern = /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;

    if (!emailPattern.test(paramValue)) {
      throw new Error(`Invalid email address provided for parameter at index ${parameterIndex}`);
    }

    return originalMethod.apply(this, args);
  };
}

class ExampleClass {
  // Apply the parameter decorator to validate email parameter
  sendEmail(@ValidateEmail email: string) {
    console.log(`Sending email to ${email}`);
  }
}

const exampleInstance = new ExampleClass();

// This will work
exampleInstance.sendEmail("example@email.com");

// This will throw an error due to email validation
try {
  exampleInstance.sendEmail("invalid-email");
} catch (error) {
  console.error(error.message); // Invalid email address provided for parameter at index 0
}
```

