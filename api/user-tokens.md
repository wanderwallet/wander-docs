---
description: Wander Injected API userTokens() function
---

# User Tokens

Some applications may request access to the tokens in your wallet and their associated balances. The `userTokens()` function returns the [result](user-tokens.md#result) from the API call.

| Argument   | Type                                          | Description                             |
| ---------- | --------------------------------------------- | --------------------------------------- |
| `options?` | [`UserTokensOptions`](user-tokens.md#options) | Optional settings for balance inclusion |

{% hint style="info" %}
**Note:** This function requires the [`ACCESS_TOKENS`](connect.md#permissions) permission.
{% endhint %}

{% hint style="info" %}
**Note:** The `options` argument is optional. If not provided, the balance will not be included in the result.
{% endhint %}

## Options

Currently Wander allows you to customize the balance fetching behavior (`false` by default):

```typescript
export interface UserTokensOptions {
  fetchBalance?: boolean;
}
```

## Result

The `userTokens()` function returns an array of token information objects. If the `fetchBalance` option is set to `true`, each token object will include its balance. The `balance` property of the token object may be `null` if there is an issue retrieving it.

```typescript
export type UserTokensResult = Array<{
  Name?: string;
  Ticker?: string;
  Logo?: string;
  Denomination: number;
  processId: string;
  balance?: string | null;
}>
```

## Example usage

```ts
// Connect to the extension and request access to the ACCESS_TOKENS permission
await window.arweaveWallet.connect(["ACCESS_TOKENS"]);

// Retrieve the list of tokens owned by the user
const tokens = await window.arweaveWallet.userTokens();
console.log("Tokens owned by the user:", tokens);

// Retrieve the list of tokens owned by the user, including their balances
const tokensWithBalances = await window.arweaveWallet.userTokens({ fetchBalance: true });
console.log("Tokens with their balances:", tokensWithBalances);
```
