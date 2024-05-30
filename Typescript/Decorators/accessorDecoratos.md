#### [Back](./README.md)

# Accessor Decorators
An Accessor Decorator is declared just before an accessor declaration. The accessor decorator is applied to the Property Descriptor for the accessor and can be used to observe, modify, or replace an accessor’s definitions. An accessor decorator cannot be used in a declaration file, or in any other ambient context (such as in a declare class).

```typescript
class Point {
  private _x: number;
  constructor(x: number, y: number) {
    this._x = x;
  }
 
  @configurable(false)
  get x() {
    return this._x;
  } 
}


function configurable(value: boolean) {
  return function (target: any, propertyKey: string, descriptor: PropertyDescriptor) {
    descriptor.configurable = value;
  };
}
```
