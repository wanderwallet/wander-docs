---
description: ArConnect Injected API encrypt() function
---

# Encrypt

Some applications (such as private file storage apps, mail clients, messaging platforms) might want to upload content to Arweave that is encrypted and only accessible by the user via their private key. The `encrypt()` function does just that: it encrypts data with the active private key and returns the encrypted bytes, similarly to the [webcrypto encrypt API](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/encrypt).

| Argument    | Type                                                                                                                                                                                                                                                                                                                                     | Description                                                                        |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| `data`      | [`ArrayBuffer`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/ArrayBuffer), [`TypedArray`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/TypedArray) or [`DataView`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/DataView) | The data to be encrypted with the user's private key                               |
| `algorithm` | [`RsaOaepParams`](https://developer.mozilla.org/en-US/docs/Web/API/RsaOaepParams), [`AesCtrParams`](https://developer.mozilla.org/en-US/docs/Web/API/AesCtrParams), [`AesCbcParams`](https://developer.mozilla.org/en-US/docs/Web/API/AesCbcParams) or [`AesGcmParams`](https://developer.mozilla.org/en-US/docs/Web/API/AesGcmParams)   | An object specifying the algorithm to be used and any extra parameters if required |

{% hint style="info" %}
**Note:** This function requires the [`ENCRYPT`](connect.md#permissions) permission.
{% endhint %}

## Example usage

```typescript
// connect to the extension
await window.arweaveWallet.connect(["ENCRYPT"]);

// encrypt data using RSA-OAEP
const encrypted = await arweaveWallet.encrypt(
    new TextEncoder().encode("This message will be encrypted"),
    { name: "RSA-OAEP" }
);

console.log("Encrypted bytes:", encrypted);
```

### Old (deprecated) usage

```ts
// connect to the extension
await window.arweaveWallet.connect(["ENCRYPT"]);

// encrypt data
const encrypted = await window.arweaveWallet.encrypt(
  new TextEncoder().encode("This message will be encrypted"),
  {
    algorithm: "RSA-OAEP",
    hash: "SHA-256",
  }
);

console.log("Encrypted bytes", encrypted);
```
