---
description: ArConnect Injected API getArweaveConfig() function
---

# Retrive Gateway Config

It can be useful to know what Arweave gateway the extension uses for your application. You can set this when [connecting](connect.md#custom-gateway-config) your application to ArConnect, but the user can always update it later. Using the `getArweaveConfig()`, you can make sure your application works, no matter what gateway the extension uses.

{% hint style="info" %}
**Note:** This function requires the [`ACCESS_ARWEAVE_CONFIG`](connect.md#permissions) permission.
{% endhint %}

## Example usage

```ts
import Arweave from "arweave";

// connect to the extension
await window.arweaveWallet.connect(["ACCESS_ARWEAVE_CONFIG"]);

// get the current gateway
const gateway = await window.arweaveWallet.getArweaveConfig();

// setup an arweave-js client using
// the obtained gateway 
const client = new Arweave(gateway);
```
