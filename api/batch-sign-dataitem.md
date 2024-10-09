---
description: ArConnect Injected API batchSignDataItem() function
---

# Batch Sign DataItem

The batchSignDataItem() function allows you to create and sign an array of data item objects, compatible with [`arbundles`](https://npmjs.com/arbundles). These data items can then be submitted to an [ANS-104](https://github.com/ArweaveTeam/arweave-standards/blob/master/ans/ANS-104.md) compatible bundler.

| Argument    | Type                                             | Description                    |
| ----------- | ------------------------------------------------ | ------------------------------ |
| `dataItems` | [`DataItem[]`](batch-sign-dataitem.md#data-item) | An array of data items to sign |

{% hint style="info" %}
**Note:** This function requires the [`SIGN_TRANSACTION`](sign.md) permission.
{% endhint %}

{% hint style="warning" %}
**Warning:** This function is designed to sign multiple small data items. There is a limit of 200kb total for the function. Please ensure that the combined size of all data items does not exceed this limit.
{% endhint %}

{% hint style="warning" %}
**Warning:** The function returns an array of buffers of the signed data items. You'll need to manually load them into an [`arbundles`](https://npmjs.com/arbundles) `DataItem` instance as seen in the [example usage](batch-sign-dataitem.md#example-usage).
{% endhint %}

## Data item

This function requires valid data item objects, like so:

```typescript
export interface DataItem[] {
  data: string | Uint8Array;
  target?: string;
  anchor?: string;
  tags?: {
    name: string;
    value: string;
  }[];
}
```

## Example usage

```ts
import { DataItem } from "arbundles";

// connect to the extension
await window.arweaveWallet.connect(["SIGN_TRANSACTION"]);

// sign the data item
const signed = await window.arweaveWallet.batchSignDataItem([
  {
    data: "This is an example transaction 1",
    tags: [
      {
        name: "Content-Type",
        value: "text/plain",
      },
    ],
  },
  {
    data: "This is an example transaction 2",
    tags: [
      {
        name: "Content-Type",
        value: "text/plain",
      },
    ],
  },
]);

// load the result into a DataItem instance
const dataItems = signed.map((buffer) => new DataItem(buffer));

// now you can submit them to a bundler
for (const dataItem of dataItems) {
  await fetch(`https://upload.ardrive.io/v1/tx`, {
    method: "POST",
    headers: {
      "Content-Type": "application/octet-stream",
    },
    body: dataItem.getRaw(),
  });
}
```
