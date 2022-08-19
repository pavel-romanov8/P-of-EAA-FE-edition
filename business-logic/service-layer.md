# Service layer

## Description 
[Pattern description](https://martinfowler.com/eaaCatalog/serviceLayer.html)

There might 2 variations of the pattern:

- Thin layer that creates domain facade
- Operations script

Operations script stands for thick classes of services which encapsulates app logic inside, but
using domain classes for domain logic. Usually we are facing the _operations script_ during
development on the FE, so the example concentrates on it rather than domain facade.

## Example

We are taking example of domain model that is described in the [domain-model.md](./domain-model.md)
and [data mapper](../data-sources/data-mapper.md).

```ts
class OrderService {

  getOrder(id: Order['id']) {
    return fetch(`https://order-store/${id}`);
  }

  async getAvailableOrders() {
    const orders = await fetch(`https://order-store/`);

    // In order to decide whether order is available or not we are referring to domain logic `order.isAvailable()`;
    return orders.map(order => orderMapper.mapFrom(order)).filter(order => order.isAvailable());
  }
}
```

We can also notice that `getAvailableOrders` method is in fact a [transaction script](./transaction-script.md) and
it is totally okay to mix transactions scripts domain model patterns simply because domain model should contain business
logic only.

## Drawbacks

The service layer leverages _transaction script_ and _domain model_ with the best of these 2 worlds. Unfortunately 
it might lead to over complicated app flow, especially for those that doesn't have much business logic and logic overall.
