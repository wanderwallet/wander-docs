---
description: ArConnect Injected API disconnect() function
---

# Disconnect

To end the current ArConnect session for the user, you can disconnect from the extension, using the `disconnect()` function. This removes all permissions from your site and ArConnect will no longer store application and gateway data related to your application. To use the Injected API again, you'll need to [reconnect](connect.md).

{% hint style="info" %}
**Note:** It is recommended to only use this function once the user clicks a clearly marked "Disconnect" button in your application.
{% endhint %}

## Example usage

```ts
// connect to the extension
await window.arweaveWallet.connect(["ACCESS_ADDRESS", "SIGN_TRANSACTION"]);

// disconnect from the extension
await window.arweaveWallet.disconnect();
```
