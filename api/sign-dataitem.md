---
description: ArConnect Injected API signDataItem() function
---

# Sign DataItem

The signDataItem() function allows you to create and sign a data item object, compatible with [`arbundles`](https://npmjs.com/arbundles). These data items can then be submitted to an [ANS-104](https://github.com/ArweaveTeam/arweave-standards/blob/master/ans/ANS-104.md) compatible bundler.

| Argument   | Type                                     | Description                   |
| ---------- | ---------------------------------------- | ----------------------------- |
| `dataItem` | [`DataItem`](sign-dataitem.md#data-item) | The bundled data item to sign |

{% hint style="info" %}
**Note:** This function requires the [`SIGN_TRANSACTION`](sign.md) permission.
{% endhint %}

{% hint style="warning" %}
**Warning:** The function returns a buffer of the signed data item. You'll need to manually load it into an [`arbundles`](https://npmjs.com/arbundles) `DataItem` instance as seen in the [example usage](sign-dataitem.md#example-usage).
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
import { DataItem } from "arbundles";

// connect to the extension
await window.arweaveWallet.connect(["SIGN_TRANSACTION"]);

// sign the data item
const signed = await window.arweaveWallet.signDataItem({
    data: "This is an example data",
    tags: [{
        name: "Content-Type",
        value: "text/plain"
    }]
});

// load the result into a DataItem instance
const dataItem = new DataItem(signed);

// now you can submit it to a bunder
await fetch(`https://node2.bundlr.network/tx`, {
    method: "POST",
    headers: {
        "Content-Type": "application/octet-stream"
    },
    body: dataItem.getRaw()
});
```
