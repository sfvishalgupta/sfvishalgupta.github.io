#### [Back](./README.md)

# Property Decorators
A Property Decorator is declared just before a property declaration. A property decorator cannot be used in a declaration file, or in any other ambient context (such as in a declare class).

The expression for the property decorator will be called as a function at runtime, with the following two arguments:

Either the constructor function of the class for a static member, or the prototype of the class for an instance member.
The name of the member.

```typescript
// Property Decorator for Email Validation
function ValidateEmail(target: any, propertyKey: string) {
  const privateFieldName = `_${propertyKey}`;

  // Store the original setter method
  const originalSetter = Object.getOwnPropertyDescriptor(target, propertyKey)?.set;

  // Define a new setter for the property
  const newSetter = function (value: any) {
    if (!isValidEmail(value)) {
      throw new Error(`Invalid email address for property "${propertyKey}".`);
    }
    this[privateFieldName] = value;
  };

  // Replace the property's setter method
  Object.defineProperty(target, propertyKey, {
    set: newSetter,
    get() {
      return this[privateFieldName];
    },
    enumerable: true,
    configurable: true,
  });
}

// Helper function to validate email addresses
function isValidEmail(email: string): boolean {
  // Regular expression for a simple email validation
  const emailPattern = /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;
  return emailPattern.test(email);
}

class User {
  @ValidateEmail
  email: string = 'test@example.com';

  constructor(email: string) {
    this.email = email;
  }
}

const user = new User('john@example.com');

console.log(user.email); // john@example.com

try {
  user.email = 'invalid-email'; // This will throw an error
} catch (error) {
  console.error(error.message); // Invalid email address for property "email".
}

// Output: 
john@example.com
Invalid email address for property "email".
```