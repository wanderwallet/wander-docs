---
description: ArConnect Injected API decrypt() function
---

# Decrypt

Data [encrypted with the user's wallet](encrypt.md) should be accessible by the owner of the private key. The `decrypt()` function allows applications to decrypt any piece of data encrypted with the user's private key, similarly to the [webcrypto encrypt API](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/decrypt).

| Argument    | Type                                                                                                                                                                                                                                                                                                                                     | Description                                                                        |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| `data`      | [`ArrayBuffer`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/ArrayBuffer), [`TypedArray`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/TypedArray) or [`DataView`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/DataView) | The encrypted data to be decrypted with the user's private key                     |
| `algorithm` | [`RsaOaepParams`](https://developer.mozilla.org/en-US/docs/Web/API/RsaOaepParams), [`AesCtrParams`](https://developer.mozilla.org/en-US/docs/Web/API/AesCtrParams), [`AesCbcParams`](https://developer.mozilla.org/en-US/docs/Web/API/AesCbcParams) or [`AesGcmParams`](https://developer.mozilla.org/en-US/docs/Web/API/AesGcmParams)   | An object specifying the algorithm to be used and any extra parameters if required |

{% hint style="info" %}
**Note:** This function requires the [`DECRYPT`](connect.md#permissions) permission.
{% endhint %}

## Example usage

```typescript
// connect to the extension
await window.arweaveWallet.connect(["ENCRYPT", "DECRYPT"]);

// encrypt data using RSA-OAEP
const encrypted = await arweaveWallet.encrypt(
    new TextEncoder().encode("This message will be encrypted"),
    { name: "RSA-OAEP" }
);

console.log("Encrypted bytes:", encrypted);

// now decrypt the same data using
// the same algorithm
const decrypted = await arweaveWallet.decrypt(
    encrypted,
    { name: "RSA-OAEP" }
);

console.log(
    "Decrypted data:",
    new TextDecoder().decode(decrypted)
);
```

### Old (deprecated) usage

```ts
// connect to the extension
await window.arweaveWallet.connect(["ENCRYPT", "DECRYPT"]);

// encrypt data
const encrypted = await window.arweaveWallet.encrypt(
  new TextEncoder().encode("This message will be encrypted"),
  {
    algorithm: "RSA-OAEP",
    hash: "SHA-256",
  }
);

console.log("Encrypted bytes:", encrypted);

// decrypt data
const decrypted = await window.arweaveWallet.decrypt(
  encrypted,
  {
    algorithm: "RSA-OAEP",
    hash: "SHA-256",
  }
);

console.log("Decrypted data:", new TextDecoder().decode(decrypted));
```
