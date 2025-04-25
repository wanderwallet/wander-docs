---
description: Wander Injected API signDataItem() function
---

# Sign DataItem

The signDataItem() function allows you to create and sign a data item object, compatible with [`arbundles`](https://www.npmjs.com/package/@dha-team/arbundles). These data items can then be submitted to an [ANS-104](https://github.com/ArweaveTeam/arweave-standards/blob/master/ans/ANS-104.md) compatible bundler.

| Argument   | Type                                                                                                                     | Description                           |
| ---------- | ------------------------------------------------------------------------------------------------------------------------ | ------------------------------------- |
| `dataItem` | [`DataItem`](sign-dataitem.md#data-item)                                                                                 | The bundled data item to sign         |
| `options?` | [`SignatureOptions`](https://github.com/ArweaveTeam/arweave-js/blob/master/src/common/lib/crypto/crypto-interface.ts#L3) | Arweave transaction signature options |

{% hint style="info" %}
**Note:** This function requires the [`SIGN_TRANSACTION`](connect.md#permissions) permission.
{% endhint %}

{% hint style="info" %}
**Note:** The `options` argument is optional, if it is not provided, the extension will use the default signature options (default salt length) to sign the transaction.
{% endhint %}

{% hint style="warning" %}
**Warning:** The function returns a buffer of the signed data item. You'll need to manually load it into an [`arbundles`](https://www.npmjs.com/package/@dha-team/arbundles) `DataItem` instance as seen in the [example usage](sign-dataitem.md#example-usage).
{% endhint %}

## Data item

This function requires a valid data item object, like so:

```typescript
export interface DataItem {
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
import { DataItem } from "@dha-team/arbundles";

// connect to the extension
await window.arweaveWallet.connect(["SIGN_TRANSACTION"]);

// sign the data item
const signed = await window.arweaveWallet.signDataItem({
  data: "This is an example data",
  tags: [
    {
      name: "Content-Type",
      value: "text/plain",
    },
  ],
});

// load the result into a DataItem instance
const dataItem = new DataItem(signed);

// now you can submit it to a bunder
await fetch(`https://upload.ardrive.io/v1/tx`, {
  method: "POST",
  headers: {
    "Content-Type": "application/octet-stream",
  },
  body: dataItem.getRaw(),
});
```
