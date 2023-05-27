---
description: ArConnect Injected API signature() function
---

# ✍ Crypto Signature

Often an application might need a piece of data that is created, authorized or confirmed by the owner of a wallet. The `signature()` function creates a cryptographical signature that allows applications to verify if a piece of data has been signed using a specific wallet. This function works similarly to the [webcrypto sign API](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/sign).

| Argument      | Type                                                       | Description                                                                       |
| ------------- | ---------------------------------------------------------- | --------------------------------------------------------------------------------- |
| `data` | [`ArrayBuffer`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer), [`TypedArray`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypedArray) or [`DataView`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/DataView) | The encrypted data to be signed with the user's private key |
| `algorithm` | [`RsaPssParams`](https://developer.mozilla.org/en-US/docs/Web/API/RsaPssParams), `AesCmacParams` or [`EcdsaParams`](https://developer.mozilla.org/en-US/docs/Web/API/EcdsaParams) | An object specifying the algorithm to be used and any extra parameters if required |

{% hint style="info" %}
**Note:** This function requires the [`SIGNATURE`](connect.md#permissions) permission.
{% endhint %}

{% hint style="warning" %}
**Note:** Not to be confused with the [`sign()`](sign.md) function that is created to sign Arweave transactions.
{% endhint %}

## Example usage

```ts
// connect to the extension
await window.arweaveWallet.connect(["SIGNATURE"]);

// sign data
const signature = await window.arweaveWallet.signature(new TextEncoder().encode("Data to sign"), {
  name: 'RSA-PSS',
  saltLength: 0,
});

console.log("The signature is", signature)
```
