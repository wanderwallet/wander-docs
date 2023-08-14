---
description: ArConnect Injected API isTokenAdded() function
---

# Check token added

When trying to [add a token](add-token.md), it can be useful to know if a token has already been added to ArConnect. The `isTokenAdded()` function returns a boolean indicating whether the token with the supplied ID has been added to the extension or not.

| Argument | Type     | Description                  |
| -------- | -------- | ---------------------------- |
| `id`     | `string` | The contract ID of the token |

{% hint style="info" %}
**Note:** This function does not require any permissions or the app to be connected to ArConnect.
{% endhint %}

## Example usage

```ts
// the ID of the token
const tokenID = "-8A6RexFkpfWwuyVO98wzSFZh0d6VJuI-buTJvlwOJQ";

// check if the token has been added
const isAdded = await window.arweaveWallet.isTokenAdded(tokenID);

// add token if it hasn't been added yet
if (!isAdded) {
  await window.arweaveWallet.addToken(tokenID);
}
```
