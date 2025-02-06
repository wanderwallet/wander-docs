---
description: Wander Injected API getActiveAddress() function
---

# Get active address

In order to identify the user's wallet, your application might need to obtain their crypto address. Arweave addresses are derived from the user's public key. The `getActiveAddress()` function returns the address that belongs to the wallet that is currently being used in Wander.

{% hint style="info" %}
**Note:** This function requires the [`ACCESS_ADDRESS`](connect.md#permissions) permission.
{% endhint %}

## Example usage

```ts
// connect to the extension
await window.arweaveWallet.connect(["ACCESS_ADDRESS"]);

// obtain the user's wallet address
const userAddress = await window.arweaveWallet.getActiveAddress();

console.log("Your wallet address is", userAddress);
```
