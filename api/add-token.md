---
description: ArConnect Injected API addToken() function
---

# Add token

In the new ArConnect version, the extension only shows tokens that the user has added. Tokens can be added via the `addToken()` function, after the user has approved it.

| Argument | Type                         | Description                                             |
| -------- | ---------------------------- | ------------------------------------------------------- |
| `id`     | `string`                     | The contract ID of the token to add to ArConnect        |
| `type?`  | `"asset"` or `"collectible"` | Type of the token (determinates how it'll be displayed) |
| `dre?`   | `string`                     | Custom DRE node (url) to load the token state with      |

{% hint style="info" %}
**Note:** This function does not require any permissions or the app to be connected to ArConnect.
{% endhint %}

{% hint style="info" %}
**Note:** The `type` argument is optional, if it is not provided, the extension will try to guess it.
{% endhint %}

{% hint style="info" %}
**Note:** The `dre` argument is optional, if it is not provided, the extension will find an appropriate DRE node from a pre-determined list of nodes. This DRE node will also automatically change, should the provided node no longer return the state of the token.
{% endhint %}

{% hint style="info" %}
**Note:** You can check if a token has been added with the [`isTokenAdded()`](is-token-added.md) function.
{% endhint %}

## Example usage

```ts
// add a token
await window.arweaveWallet.addToken("-8A6RexFkpfWwuyVO98wzSFZh0d6VJuI-buTJvlwOJQ");

// add a token with a pre-defined type
await window.arweaveWallet.addToken(
  "rjyDN_VlSl4b_Cqn6nfE6tMMZhTJq0RGMFxGhvsefMc",
  "collectible"
);

// add a token with a custom dre node
await window.arweaveWallet.addToken(
  "rjyDN_VlSl4b_Cqn6nfE6tMMZhTJq0RGMFxGhvsefMc",
  "collectible",
  "https://dre-4.warp.cc"
);
```
