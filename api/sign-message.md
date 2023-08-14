---
description: ArConnect Injected API signMessage() function
---

# Sign message

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
**Note**: The function first hashes the input data for security reasons. We recommend using the built in [`verifyMessage()`](verify-message.md) function to validate the signature, or hashing the data the same way, before validation ([example](sign-message.md#verification-without-arconnect)).
{% endhint %}

{% hint style="info" %}
**Note:** The `options` argument is optional, if it is not provided, the extension will use the default signature options (default hash algorithm: `SHA-256`) to sign the data.
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

// message to be signed
const data = new TextEncoder().encode("The hash of this msg will be signed.");

// create signature
const signature = await window.arweaveWallet.signMessage(data);

// verify signature
const isValidSignature = await window.arweaveWallet.verifyMessage(data, signature);

console.log(`The signature is ${isValidSignature ? "valid" : "invalid"}`);
```

## Verification without ArConnect

You might encounter situations where you need to verify the signed message against an ArConnect generated signature, but the extension is not accessible or not installed (for e.g.: server side code, unsupported browser, etc.).

In these cases it is possible to validate the signature by hashing the message (with the algorithm you used when generating the signature through ArConnect) and verifying that against the ArConnect signature. This requires the message to be verified, the signature and the [wallet's public key](get-active-public-key.md). Below is the JavaScript (TypeScript) example implementation with the [Web Crypto API](https://developer.mozilla.org/en-US/docs/Web/API/Web\_Crypto\_API), using `SHA-256` hashing:

```typescript
// connect to the extension
await window.arweaveWallet.connect(["SIGNATURE"]);

// message to be signed
const data = new TextEncoder().encode("The hash of this msg will be signed.");

// create signature
const signature = await window.arweaveWallet.signMessage(data);

/** This is where we start the verification **/
// hash the message (we used the default signMessage() options
// so the extension hashed the message using "SHA-256"
const hash = await crypto.subtle.digest("SHA-256", data);

// import public JWK
// we need the user's public key for this
const publicJWK: JsonWebKey = {
    e: "AQAB",
    ext: true,
    kty: "RSA",
    // !! You need to obtain this on your own !!
    // possible ways are: 
    // - getting from ArConnect if available
    // - storing it beforehand
    // - if the wallet has made any transactions on the Arweave network
    //   the public key is going to be the owner field of the mentioned
    //   transactions
    n: publicKey
};

// import public jwk for verification
const verificationKey = await crypto.subtle.importKey(
    "jwk",
    publicJWK,
    {
      name: "RSA-PSS",
      hash: "SHA-256"
    },
    false,
    ["verify"]
);

// verify the signature by matching it with the hash
const isValidSignature = await crypto.subtle.verify(
    { name: "RSA-PSS", saltLength: 32 },
    verificationKey,
    signature,
    hash
);

console.log(`The signature is ${isValidSignature ? "valid" : "invalid"}`);
```
