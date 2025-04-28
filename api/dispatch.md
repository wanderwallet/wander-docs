---
description: Wander Injected API dispatch() function
---

# Dispatch Transaction

The `dispatch()` function allows you to quickly sign and send a transaction to the network in a bundled format. It is best for smaller datas and contract interactions. If the bundled transaction cannot be submitted, it will fall back to a base layer transaction. The function returns the [result](dispatch.md#dispatch-result) of the API call.

| Argument      | Type                                                                                                                     | Description                                                  |
| ------------- | ------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------ |
| `transaction` | [`Transaction`](https://github.com/arweaveTeam/arweave-js#transactions)                                                  | A valid Arweave transaction instance (**without a keyfile**) |
| `options?`    | [`SignatureOptions`](https://github.com/ArweaveTeam/arweave-js/blob/master/src/common/lib/crypto/crypto-interface.ts#L3) | Arweave transaction signature options                        |

{% hint style="info" %}
**Note:** This function requires the [`DISPATCH`](connect.md#permissions) permission.
{% endhint %}

{% hint style="info" %}
**Note:** The `options` argument is optional, if it is not provided, the extension will use the default signature options (default salt length) to sign the transaction.
{% endhint %}

{% hint style="warning" %}
**Note:** If you are trying to sign a larger piece of data (5 MB <), make sure to notify the user to not switch / close the browser tab. Larger transactions are split into chunks in the background and will take longer to sign.
{% endhint %}

{% hint style="warning" %}
**Note:** The function uses the default bundler node set by the user or the extension. Consider using the [`signDataItem()`](sign-dataitem.md) function to submit data to a custom bundler.&#x20;
{% endhint %}

## Dispatch result

The `dispatch()` function returns the result of the operation, including the ID of the submitted transaction, as well as if it was submitted in a bundle or on the base layer.

```ts
export interface DispatchResult {
  id: string;
  type?: "BASE" | "BUNDLED";
}
```

## Example usage

```ts
import Arweave from "arweave";

// create arweave client
const arweave = new Arweave({
  host: "ar-io.net",
  port: 443,
  protocol: "https"
});

// connect to the extension
await window.arweaveWallet.connect(["DISPATCH"]);

// create a transaction
const transaction = await arweave.createTransaction({
  data: '<html><head><meta charset="UTF-8"><title>Hello permanent world! This was signed via Wander!!!</title></head><body></body></html>'
});

// dispatch the tx
const res = await window.arweaveWallet.dispatch(transaction);

console.log(`The transaction was dispatched as a ${res.type === "BUNDLED" ? "bundled" : "base layer"} Arweave transaction.`)
```
