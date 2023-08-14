---
description: ArConnect Injected API verifyMessage() function
---

# Verify message

This function allows verifying a cryptographic signature [created by ArConnect](sign-message.md).

| Argument     | Type                                            | Description                                                                                                     |
| ------------ | ----------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| `data`       | `ArrayBuffer`                                   | The data to verify the signature for                                                                            |
| `signature`  | `ArrayBuffer \| string`                         | The signature to validate                                                                                       |
| `publicKey?` | `string`                                        | Arweave wallet `JWK.n` field, transaction owner field or [public key from ArConnect](get-active-public-key.md). |
| `options?`   | [`SignMessageOptions`](sign-message.md#options) | Configuration for the signature                                                                                 |

{% hint style="info" %}
**Note:** This function requires the [`SIGNATURE`](sign.md) permission.
{% endhint %}

{% hint style="info" %}
**Note:** The `publicKey` argument is optional, if it is not provided, the extension will use the currently selected wallet's public key. You might only need this if the message to be verified was not made by the connected user.
{% endhint %}

{% hint style="info" %}
**Note:** The `options` argument is optional, if it is not provided, the extension will use the default signature options (default hash algorithm) to sign the data.
{% endhint %}

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
