---
description: ArConnect DOM events
---

# Events

ArConnect provides useful custom events to track the state of the extension. These events implement the [`CustomEvent`](https://developer.mozilla.org/en-US/docs/Web/Events/Creating\_and\_triggering\_events#adding\_custom\_data\_%E2%80%93\_customevent) browser API.

## `arweaveWalletLoaded` event

This event is dispatched once the ArConnect Injected API has been initialized in the `window` object. Before this event is fired, you cannot interact with ArConnect and the `window.arweaveWallet` object will be undefined.

### Example

```ts
addEventListener("arweaveWalletLoaded", () => {
  // now we can interact with ArConnect
  const permissions = await window.arweaveWallet.getPermissions();

  if (permissions.length <= 0) {
    await window.arweaveWallet.connect(["ACCESS_ADDRESS"]);
  }
});
```

## `walletSwitch` event

This event is fired when the user manually switches their active wallet. The even also includes the new active wallet's address, if the user allowed the `ACCESS_ADDRESS` and the `ACCESS_ALL_ADDRESSES` permissions.

### Example

```ts
addEventListener("walletSwitch", (e) => {
  const newAddress = e.detail.address;

  // handle wallet switch
});
```

## Event emitter

The event emitter is available under `window.arweaveWallet.events` as a more advanced event system for the extension.

{% hint style="info" %}
**Note:** This documentation is incomplete and the feature is experimental.
{% endhint %}
