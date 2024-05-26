---
description: ArConnect Injected API subscription() function
---

# Subscriptions

Subscriptions is a feature that allows users to subscribe to applications and be charged on a periodic basis such as monthly, weekly, or yearly. Users will be charged the moment they subscribe

| Argument                    | Type                                                                        | Description                                              |
| --------------------------- | --------------------------------------------------------------------------- | -------------------------------------------------------- |
| `arweaveAccountAddress`     | `string`                                                                    | The account address where payments will be made          |
| `applicationName`           | `string`                                                                    | The name of your application                             |
| `subscriptionName`          | `string`                                                                    | The name of the subscription                             |
| `subscriptionManagementUrl` | `string`                                                                    | A URL where users are able to manage their subscriptions |
| `subscriptionFeeAmount`     | `number`                                                                    | The amount in AR to be paid each period                  |
| `recurringPaymentFrequency` | [`RecurringPaymentFrequency`](subscriptions.md#recurring-payment-frequency) | Frequency for period to be charged                       |
| `subscriptionEndDate`       | `Date`                                                                      | When the subscription ends                               |
| `applicationIcon`           | `string`                                                                    | URL where an image is hosted, ideally 48x48              |

{% hint style="info" %}
**Note:** This function requires the [`ACCESS_ALL_ADDRESSES`](connect.md#permissions) permission.
{% endhint %}

## Recurring Payment Frequency

This function requires a recurring frequency such as listed:

Recurring Payment Frequency

```typescript
export enum RecurringPaymentFrequency {
  ANNUALLY = "Annually",
  QUARTERLY = "Quarterly",
  MONTHLY = "Monthly",
  WEEKLY = "Weekly",
  DAILY = "Daily",
}
```

## Example usage

```ts
// connect to the extension
await window.arweaveWallet.connect(["ACCESS_ALL_ADDRESSES"]);

// sign the data item
const subscription = await window.arweaveWallet.subscription({
  arweaveAccountAddress: "hY70z-mbKfDByqXh4y43ybSxReFVo1i9lB1dDdCkO_U",
  applicationName: "ArConnect",
  subscriptionName: "ArConnect Premium",
  subscriptionManagementUrl: "https://www.arconnect.io/premium",
  subscriptionFeeAmount: 0.5,
  recurringPaymentFrequency: "Monthly",
  subscriptionEndDate: new Date("2024-12-31"),
  applicationIcon: "https://www.arconnect.io/logo",
});

// Subscription will output the details and the initial payment txn
console.log("Subscription details with paymentHistory array:", subscription);
```
