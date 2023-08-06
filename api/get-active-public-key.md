---
description: ArConnect Injected API getActivePublicKey() function
---

# Get active public key

This function allows you to get the public key of the currently active wallet in ArConnect.

{% hint style="info" %}
**Note:** This function requires the [`ACCESS_PUBLIC_KEY`](connect.md#permissions) permission.
{% endhint %}

## Example usage

```ts
// connect to the extension
await window.arweaveWallet.connect(["ACCESS_PUBLIC_KEY"]);

// obtain the user's public key
const publicKey = await window.arweaveWallet.getActivePublicKey();

console.log("JWK.n field is:", publicKey);

// create public key JWK
const publicJWK: JsonWebKey = {
    e: "AQAB",
    ext: true,
    kty: "RSA",
    n: publicKey
};

// import it with webcrypto, etc.
```
