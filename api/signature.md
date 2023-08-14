---
description: ArConnect Injected API signature() function
---

# Crypto signature

{% hint style="danger" %}
**Deprecation warning:** The `signature()` function is deprecated in ArConnect 1.0.0. Read about the alternatives below.
{% endhint %}

## Alternatives

There are quite a few cases where you might need to generate a cryptographic signature for a piece of data or message so that you can verify them. The most common ones and their alternatives are the following:

* Generating a signature for a transaction: [`sign()`](sign.md)
* Generating a signature for a bundle data item: [`signDataItem()`](sign-dataitem.md) or [`dispatch()`](dispatch.md)
* Signing a message to later validate ownership: [`signMessage()`](sign-message.md) combined with [`verifyMessage()`](verify-message.md)

The safety of our users' wallets is our top priority, so we've decided to deprecate our `signature()` function, following the example of _Arweave.app_ and we expect other Arweave wallets now or in the future to do the same, so eventually, this should be a smooth transition to the new alternatives. We are sorry for any inconveniences caused by this change.

~~Often an application might need a piece of data that is created, authorized or confirmed by the owner of a wallet. The `signature()` function creates a cryptographical signature that allows applications to verify if a piece of data has been signed using a specific wallet. This function works similarly to the~~ [~~webcrypto sign API~~](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/sign)~~.~~

| Argument        | Type                                                                                                                                                                                                                                                                                                                                                         | Description                                                                            |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------- |
| ~~`data`~~      | [~~`ArrayBuffer`~~](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/ArrayBuffer)~~,~~ [~~`TypedArray`~~](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/TypedArray) ~~or~~ [~~`DataView`~~](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global\_Objects/DataView) | ~~The encrypted data to be signed with the user's private key~~                        |
| ~~`algorithm`~~ | [~~`RsaPssParams`~~](https://developer.mozilla.org/en-US/docs/Web/API/RsaPssParams)~~, `AesCmacParams` or~~ [~~`EcdsaParams`~~](https://developer.mozilla.org/en-US/docs/Web/API/EcdsaParams)                                                                                                                                                                | ~~An object specifying the algorithm to be used and any extra parameters if required~~ |

{% hint style="info" %}
~~**Note:** This function requires the~~ [~~`SIGNATURE`~~](connect.md#permissions) ~~permission.~~
{% endhint %}

{% hint style="warning" %}
~~**Note:** Not to be confused with the~~ [~~`sign()`~~](sign.md) ~~function that is created to sign Arweave transactions.~~
{% endhint %}

## ~~Example usage~~

```ts
// connect to the extension
await window.arweaveWallet.connect(["SIGNATURE"]);

// sign data
const signature = await window.arweaveWallet.signature(new TextEncoder().encode("Data to sign"), {
  name: 'RSA-PSS',
  saltLength: 0,
});

console.log("The signature is", signature);
```
