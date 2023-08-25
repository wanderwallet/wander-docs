---
description: ArConnect Injected API sign() function
---

# Sign Transaction

To submit a transaction to the Arweave Network, it first has to be signed using a private key. The `sign()` function is meant to replicate the behavior of the `transactions.sign()` function of [`arweave-js`](https://github.com/arweaveTeam/arweave-js#sign-a-transaction), but instead of mutating the transaction object, it returns a new and signed transaction instance.

| Argument      | Type                                                                                                                     | Description                                                  |
| ------------- | ------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------ |
| `transaction` | [`Transaction`](https://github.com/arweaveTeam/arweave-js#transactions)                                                  | A valid Arweave transaction instance (**without a keyfile**) |
| `options?`    | [`SignatureOptions`](https://github.com/ArweaveTeam/arweave-js/blob/master/src/common/lib/crypto/crypto-interface.ts#L3) | Arweave transaction signature options                        |

{% hint style="info" %}
**Note:** This function requires the [`SIGN_TRANSACTION`](connect.md#permissions) permission.
{% endhint %}

{% hint style="info" %}
**Note:** The `options` argument is optional, if it is not provided, the extension will use the default signature options (default salt length) to sign the transaction.
{% endhint %}

{% hint style="warning" %}
**Tip:** A better alternative to this function is using the [`arweave-js`](https://github.com/arweaveTeam/arweave-js#sign-a-transaction) `transactions.sign()` instead. Just omit the second parameter (`JWK` key) when calling the method, and [`arweave-js`](https://github.com/arweaveTeam/arweave-js#sign-a-transaction) will automatically use ArConnect.
{% endhint %}

{% hint style="warning" %}
**Note:** If you are trying to sign a larger piece of data (5 MB <), make sure to notify the user to not switch / close the browser tab. Larger transactions are split into chunks in the background and will take longer to sign.
{% endhint %}

## Example usage

### With `arweave-js` (recommended)

```ts
import Arweave from "arweave";

// create arweave client
const arweave = new Arweave({
  host: "ar-io.net",
  port: 443,
  protocol: "https"
});

// connect to the extension
await window.arweaveWallet.connect(["SIGN_TRANSACTION"]);

// create a transaction
const transaction = await arweave.createTransaction({
  data: '<html><head><meta charset="UTF-8"><title>Hello permanent world! This was signed via ArConnect!!!</title></head><body></body></html>'
});

// sign using arweave-js
await arweave.transactions.sign(transaction);

// TODO: post the transaction to the network
```

### Directly using ArConnect

```ts
import Arweave from "arweave";

// create arweave client
const arweave = new Arweave({
  host: "ar-io.net",
  port: 443,
  protocol: "https"
});

// connect to the extension
await window.arweaveWallet.connect(["SIGN_TRANSACTION"]);

// create a transaction
let transaction = await arweave.createTransaction({
  data: '<html><head><meta charset="UTF-8"><title>Hello permanent world! This was signed via ArConnect!!!</title></head><body></body></html>'
});

// sign using arweave-js
transaction = await window.arweaveWallet.sign(transaction);

// TODO: post the transaction to the network
```
