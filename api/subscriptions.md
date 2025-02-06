---
description: Wander Injected API subscription() function
---

# Subscriptions

Subscriptions is a feature that allows users to subscribe to applications and be charged on a periodic basis such as monthly, weekly, or quarterly. Users will be charged the moment they subscribe

<table><thead><tr><th width="283">Argument</th><th width="278">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>arweaveAccountAddress</code></td><td><code>string</code></td><td>The account address where payments will be made</td></tr><tr><td><code>applicationName</code></td><td><code>string</code></td><td>The name of your application</td></tr><tr><td><code>subscriptionName</code></td><td><code>string</code></td><td>The name of the subscription</td></tr><tr><td><code>subscriptionManagementUrl</code></td><td><code>string</code></td><td>A URL where users are able to manage their subscriptions</td></tr><tr><td><code>subscriptionFeeAmount</code></td><td><code>number</code></td><td>The amount in AR to be paid each period</td></tr><tr><td><code>recurringPaymentFrequency</code></td><td><a href="subscriptions.md#recurring-payment-frequency"><code>RecurringPaymentFrequency</code></a></td><td>Frequency for period to be charged</td></tr><tr><td><code>subscriptionEndDate</code></td><td><code>Date</code></td><td>When the subscription ends</td></tr><tr><td><code>applicationIcon</code></td><td><code>string</code></td><td>URL where an image is hosted, ideally 48x48</td></tr></tbody></table>

{% hint style="info" %}
**Note:** This function requires the [`ACCESS_ALL_ADDRESSES`](connect.md#permissions) permission.
{% endhint %}

## Recurring Payment Frequency

This function requires a recurring frequency such as listed:

Recurring Payment Frequency

```typescript
export enum RecurringPaymentFrequency {
  QUARTERLY = "Quarterly",
  MONTHLY = "Monthly",
  WEEKLY = "Weekly",
  DAILY = "Daily",
}
```

## Example usage

{% hint style="info" %}
_Wander was formerly know as ArConnect. There are some API references that still use ArConnect_
{% endhint %}

```ts
// connect to the extension
await window.arweaveWallet.connect(["ACCESS_ALL_ADDRESSES"]);

// submit the subscription information
const subscription = await window.arweaveWallet.subscription({
  arweaveAccountAddress: "hY70z-mbKfDByqXh4y43ybSxReFVo1i9lB1dDdCkO_U",
  applicationName: "Wander",
  subscriptionName: "Wander Premium",
  subscriptionManagementUrl: "https://wander.app/premium",
  subscriptionFeeAmount: 0.5,
  recurringPaymentFrequency: "Monthly",
  subscriptionEndDate: new Date("2024-12-31"),
  applicationIcon: "https://wander.app/logo",
});

// Subscription will output the details and the initial payment txn
console.log("Subscription details with paymentHistory array:", subscription);
```
