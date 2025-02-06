---
description: Wander Injected API getAllAddresses() function
---

# Get all addresses

Wander provides enhanced key management for your Arweave wallets. Because of this, the extension might store more than one wallet and your application can take advantage of that. For example, this feature can make it easier for your app to transfer tokens between the user's addresses. The `getAllAddresses()` function returns an array of addresses added to Wander.

{% hint style="info" %}
**Note:** This function requires the [`ACCESS_ALL_ADDRESSES`](connect.md#permissions) permission.
{% endhint %}

## Example usage

```ts
// connect to the extension
await window.arweaveWallet.connect(["ACCESS_ADDRESS", "ACCESS_ALL_ADDRESSES"]);

// get all wallet addresses added to ArConnect
const addresses = await window.arweaveWallet.getAllAddresses();

// obtain the user's active wallet address
const activeAddress = await window.arweaveWallet.getActiveAddress();

console.log("Your wallet address is", activeAddress);
console.log("You can transfer your assets to your other addresses:\n", addresses.filter((addr) => addr !== activeAddress).join("\n"));
```
