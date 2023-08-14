---
description: ArConnect Injected API privateHash() function
---

# Private hash

The `privateHash()` function allows you to create deterministic secrets (hashes) from some data.

| Argument  | Type                                            | Description                |
| --------- | ----------------------------------------------- | -------------------------- |
| `data`    | `ArrayBuffer`                                   | The data to hash           |
| `options` | [`SignMessageOptions`](sign-message.md#options) | Configuration for the hash |

{% hint style="info" %}
**Note:** This function requires the [`SIGNATURE`](sign.md) permission.
{% endhint %}

## Example usage

```ts
// connect to the extension
await window.arweaveWallet.connect(["SIGNATURE"]);

// data to be hashed
const data = new TextEncoder().encode("The hash of this msg will be signed.");

// create the hash using the active wallet
const hash = await window.arweaveWallet.privateHash(
    data,
    { hashAlgorithm: "SHA-256" }
);

console.log("Data hash is", hash);
```
