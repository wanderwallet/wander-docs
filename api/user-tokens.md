---
description: ArConnect Injected API userTokens() function
---

# User tokens

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

Currently ArConnect allows you to customize the balance fetching behavior (`false` by default):

```typescript
export interface UserTokensOptions {
  fetchBalance?: boolean;
}
```

## Result

The `userTokens()` function returns the token information, including the balance if the `fetchBalance` option is set to `true`.

```typescript
export type UserTokensResult = Array<{
  Name?: string;
  Ticker?: string;
  Logo?: string;
  Denomination: number;
  processId?: string;
  balance?: string;
}>
```

## Example usage

```ts
// connect to the extension
await window.arweaveWallet.connect(["ACCESS_TOKENS"])

// get user tokens
await window.arweaveWallet.userTokens();

// include balance
await window.arweaveWallet.userTokens({ fetchBalance: true });
```
