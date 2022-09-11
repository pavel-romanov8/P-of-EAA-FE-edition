# Active record

## Description
[Pattern description](https://www.martinfowler.com/eaaCatalog/activeRecord.html);

## Example

```ts
class Product {

  constructor(
    private _price: number,
    private _runsOutDate: Date | null,
  ) { }

  static find(id: number) {
    return fetch(`https://api/product/${id}`);
  }

  update() {
    
    // Getting the ID from the Layer Supertype, like we did for Row Data Gateway
    return fetch(
      `https://api/product/${getId()}`,
      data: JSON.Stringify({
        price: this._price,
        runsOutDate: this._runsOutDate,
      }))
  }

  // Business logic
  isAvailable(): boolean {
    return this.runsOutDate === null;
  }
}
```

## Drawbacks

It won't be efficient enough when we have complex business logic, especially when we want to have
inheritance or work with arrays or objects because each field of active record should represent 1
record of the table. F.e. firstName - firstName