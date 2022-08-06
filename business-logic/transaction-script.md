# Transaction script

## Description
[Pattern description](https://martinfowler.com/eaaCatalog/transactionScript.html)

## Case

Let's imagine that we are some popular authors and want to sell a new book which we just finished.
For that, we are going to create a new landing page with the book presentation and form where user type his info.
After successful form submission we wan't to somehow show the user its result.

## Solution

Since the landing of 1 book is not a big deal and there won't be too much logic - transaction script is a really good option
to organize the hole business logic.

Function that will display notification to the end user:
```ts
function notify(message: string): void {
  alert(message);
}
```

One of the possible ways to organize the logic flow:
```ts
interface Customer {
  readonly firstName: string;
  readonly secondName: string;
  readonly email: string;
  readonly phoneNumber: string;
}

function async createOrderForCustomer(): Promise<void> {
  const customer = document.getElementById('customerForm').value as Customer;
  try {
    await fetch('https://my-boooks.com', {
      method: 'POST',
      body: JSON.stringify(customer),
    });
    notify('The book is ordered! Please, check your email for the next steps');
  } catch (error: unknown) {
    notify('Something goes wrong. Please try to order the book again');
  }
}
```

You can see that we don't have any layers here. One method handles the transaction from start to finish.

## Drawbacks

Transaction script is good for the simple business logic where we don't have too much to handle, but when
it comes to something bigger than book order we are certainly going to face some problems:

- Code duplication.
- Multiple sources of truth which lead us to false assumption about the logic flow at some parts of the app