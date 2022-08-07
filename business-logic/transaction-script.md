# Transaction script

## Description
[Pattern description](https://martinfowler.com/eaaCatalog/transactionScript.html)

## Solution
```ts
interface Product {
  name: string;
  price: number;
  runsOutDate: Date | null;
}

interface Order {
  products: Product[];
  orderNumber: number;
  creationDate: Date | null;
}

async function getOrder(): void {
  const order = await fetch('https://get-order.com') as Order;
  const orderContainer = document.getElementById('order');
  const isAvailableOrder = order.products.find(product => product.runsOutDate === null) != undefined;
  orderContainer.innerHtml = `
    <p>Order number: ${order.orderNumber}</p>
    <ul>
      <p>List of products: </p>
      ${order.products.map(product => {
        return `<li>${product.name} - ${product.price}</li>`
      })}
    </ul>
    <button disabled=${isAvailableOrder}>Order</button>
  `;
}
```

## Drawbacks

Transaction script is good for the simple business logic where we don't have too much to handle, but when
it comes to something bigger we are certainly going to face some problems:

- Code duplication.
- Multiple sources of truth which lead us to false assumption about the logic flow at some parts of the app.
