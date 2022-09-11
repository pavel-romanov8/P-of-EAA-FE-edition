# Row data gateway

## Description
[Pattern description](https://martinfowler.com/eaaCatalog/rowDataGateway.html)

## Example

```ts
export class OrderGetaway {

  constructor(
    private _products: Product[],
    private creationDate: Date | null,
  ) {}

  set products(products: Product[]) {
    return this._products = products;
  }

  get products() {
    return this._products;
  }

  update() {
    return fetch(

      // The row data gateway doesn't store any IDs, we are getting it from Layer Supertype.
      `https://api/orders/${getId()}`,
      {
        data: JSON.stringify({ products: this.products, creationDate: this.creationDate })
      },
    );
  }
}
```

It might be hard to distinguish cases when it is appropriate to use _Row Data Gateway_ vs _Active Record_.
The rule of thumb is - when we have any business logic inside of our gateway it becomes an _Active Record_,
otherwise it still remains as _Row Data Gateway_.

## Drawbacks
As the [table-data-gateway](./table-data-gateway.md) this pattern is pretty good when using with 
[transaction script](../business-logic/transaction-script.md). If we want to use it with [domain model](../business-logic/domain-model.md) we have 2 options:

- Use the row data gateway as a delegate within domain object.
- Copy and paste things from it to domain model object (1 more mapping is required).

Both options doesn't seem to fit well in the domain model patter.