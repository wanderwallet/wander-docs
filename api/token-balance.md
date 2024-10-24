---
description: ArConnect Injected API tokenBalance() function
---

# Token balance

Some applications may request access to the balance of a specific token in your wallet. The `tokenBalance()` function returns the balance of the token identified by its ID.

| Argument   | Type                                          | Description                             |
| ---------- | --------------------------------------------- | --------------------------------------- |
| `id` | string | The unique identifier (processId) of the token |

{% hint style="info" %}
**Note:** This function requires the [`ACCESS_TOKENS`](connect.md#permissions) permission.
{% endhint %}

## Result

The `tokenBalance()` function returns the balance of the requested token as a string.

{% hint style="warning" %}
**Note**: This function throws an error if there is an issue retrieving the balance. Please make sure to handle such cases in your code.
{% endhint %}

```typescript
export type TokenBalanceResult = string;
```

## Example usage

```ts
// Connect to the extension and request access to the ACCESS_TOKENS permission
await window.arweaveWallet.connect(["ACCESS_TOKENS"]);

// Retrieve the list of tokens owned by the user
const tokens = await window.arweaveWallet.userTokens();
console.log("Tokens owned by the user:", tokens);

try {
  // Retrieve the balance of a user token
  const tokenId = tokens[0].processId
  const balance = await window.arweaveWallet.tokenBalance(tokenId);
  console.log(`Balance of the token with ID ${tokenId}:`, balance);
} catch (error) {
  console.error("Error fetching token balance:", error);
}
```
