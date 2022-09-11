# Table data gateway

## Description
[Pattern description](https://www.martinfowler.com/eaaCatalog/tableDataGateway.html)

## Example

```ts

export class OrderGetaway {

  findAll() {
    return fetch('https://api/orders');
  }

  findOne(id: number) {
    return fetch(`https://api/orders/${id}`);
  }

  delete(id: number) {
    return fetch(`https://api/orders/${id}`, { method: 'DELETE' });
  }
}
```

We can build such abstractions over network interaction since we can treat it as some kind
of database for us. It is also possible to built this over `LocalStorage` or `IndexDB`. With `IndexDB`
it would be a canonical implementation since we are working with the DB directly. As you might notice,
the gateway class usually doesn't have any state.

## Drawbacks
The solution is quite simple and it is really handy when it comes to [transaction script](../business-logic/transaction-script.md). However if we are using [domain model](../business-logic/domain-model.md) for business logic
organization it is better to use [data mapper](./data-mapper.md), because it allows us to have better isolation.