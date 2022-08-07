# Domain model

## Description
[Pattern description](https://martinfowler.com/eaaCatalog/domainModel.html)

## Example
```ts
class Product {
  constructor(
    price: number,
    runsOutDate: Date | null,
  ) { }

  isAvailable(): boolean {
    return this.runsOutDate === null;
  }
}

class Order {
  constructor(
    products: Product[],
    creationDate: Date | null,
  ) {}

  isAvailable(): boolean {
    return this.products.find(product => !product.isAvailable()) !== undefined;
  }
}
```

The example doesn't show any work with HTML or HTTP intentionally because the pattern itself about 
encapsulation of business logic from other stuff like network communication and view.

## Drawbacks

Domain models are great when it comes to big and complex business logic. The problem we might have during usage of
the pattern is unnecessary complexity. If we do have really small domain it might be redundant to use the pattern.
