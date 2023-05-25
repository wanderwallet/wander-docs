---
description: ArConnect Injected API getWalletNames() function
---

# 🔠 Get Wallet Names

In ArConnect, each wallet has a nickname. This is either the user's [ANS](https://ans.gg) name, or a user-given nickname. To provide better UX, you can retrive these names and display them for the user, so they can easily recognize which wallet they're using. The `getWalletNames()` function returns an object, where the object keys are the wallet addresses and the values are the nicknames.

{% hint style="info" %}
**Note:** This function requires the [`ACCESS_ALL_ADDRESSES`](connect.md#permissions) permission.
{% endhint %}

## Example usage

```ts
// connect to the extension
await window.arweaveWallet.connect(["ACCESS_ADDRESS", "ACCESS_ALL_ADDRESSES"]);

// get all wallet names from ArConnect
const walletNames = await window.arweaveWallet.getWalletNames();

// obtain the user's active wallet address
const activeAddress = await window.arweaveWallet.getActiveAddress();

console.log("Your active wallet's nickname is", walletNames[activeAddress]);
```
