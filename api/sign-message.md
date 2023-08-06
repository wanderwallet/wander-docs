---
description: ArConnect Injected API signMessage() function
---

# Sign message

{% hint style="warning" %}
**Note:** The `signMessage()` function is only available in the [**ArConnect BETA**](../devtools/beta.md).
{% endhint %}

This function allows creating a cryptographic signature for any piece of data for later validation.

| Argument   | Type                                            | Description                            |
| ---------- | ----------------------------------------------- | -------------------------------------- |
| `data`     | `ArrayBuffer`                                   | The data to generate the signature for |
| `options?` | [`SignMessageOptions`](sign-message.md#options) | Configuration for the signature        |

{% hint style="info" %}
**Note:** This function requires the [`SIGNATURE`](sign.md) permission.
{% endhint %}

{% hint style="warning" %}
**Note**: This function should only be used to allow data validation. It cannot be used for on-chain transactions, interactions or bundles, for security reasons. Consider implementing [`sign()`](sign.md), [`signDataItem()`](sign-dataitem.md) or [dispatch()](dispatch.md).
{% endhint %}

{% hint style="warning" %}
**Note**: The function first hashes the input data for security reasons. We recommend using the built in [`verifyMessage()`](verify-message.md) function to validate the signature, or hashing the data the same way, before validation.
{% endhint %}

{% hint style="info" %}
**Note:** The `options` argument is optional, if it is not provided, the extension will use the default signature options (default hash algorithm) to sign the data.
{% endhint %}

## Options

Currently ArConnect allows you to customize the hash algorithm (`SHA-256` by default):

```typescript
export interface SignMessageOptions {
  hashAlgorithm?: "SHA-256" | "SHA-384" | "SHA-512";
}
```

## Example usage

```ts
// connect to the extension
await window.arweaveWallet.connect(["SIGNATURE"]);

// data to be signed
const data = new TextEncoder().encode("The hash of this msg will be signed.");

// create signature
const signature = await window.arweaveWallet.signMessage(data);

// verify signature
const isValidSignature = await window.arweaveWallet.verifyMessage(data, signature);

console.log(`The signature is ${isValidSignature ? "valid" : "invalid"}`);
```
