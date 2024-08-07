---
description: ArConnect Injected API userTokens() function
---

# User tokens

Some applications will request to access tokens added to your wallet and the balances associated with it

| Argument   | Type                                          | Description                |
| ---------- | --------------------------------------------- | -------------------------- |
| `options?` | [`UserTokensOptions`](user-tokens.md#options) | Include balance in request |

{% hint style="info" %}
**Note:** This function requires the [`ACCESS_TOKENS`](connect.md#permissions) permission.
{% endhint %}

{% hint style="info" %}
**Note:** The `options` argument is optional, if it is not provided, the balance will not be returned
{% endhint %}

## Options

Currently ArConnect allows you to customize the balance fetching behavior (`false` by default):

```typescript
export interface UserTokensOptions {
  fetchBalance?: boolean;
}
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
