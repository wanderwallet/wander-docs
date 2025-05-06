---
description: Introducing the Wander Connect Embedded Wallet for Arweave and AO
---

# Wander Connect

<div data-full-width="false"><figure><img src="../.gitbook/assets/Wander Docs-API.png" alt=""><figcaption></figcaption></figure></div>

A simplified, lightweight, customizable embedded wallet for Arweave and AO that bridges the gap between web2 and web3,
helping non-crypto native users onboard into web3 easily!

- 🪪 **Familiar Authentication:** Users sign up/in with their favorite and familiar authentication method: email and
  password, passkeys and social providers (Facebook, Twitter/X, Apple).
- 🔑 **No Seed Phrases:** 5 clicks is all it takes for your users to get to their fully functional wallet. Managing
  seed phrases and backups is an optional step that can be taken care of later.
- 📱 **Simplified UI:** De-clutter UI with all the functionality your users need, but the same functionality as the
  mighty Wander Browser Extension.
- ✨ **Refined Experience:** Light and dark themes, and responsive out-of-the-box. A wallet that works on any device
  and platform, with no download needed.

And offering a great developer experience too:

- 🔌 **Easy Integration**: Easy to use SDK to embed Wander Connect wallet in your dApp.
- 🎨 **Customizable UI**: Extensive customization and layout options. A white-label wallet that can match your
  brand & site/app's look and feel.
- 🔒 **Secure**: User keys are secured using advanced cryptography, such as AES and Shamir Secret Sharing. Neither we
  nor your app will ever get access to users' private keys.

## Installation

Use the Wander Connect SDK to integrate the Wander Connect embedded wallet in your web applications and dApps.

[![npm version](https://img.shields.io/npm/v/@wanderapp/connect.svg)](https://www.npmjs.com/package/@wanderapp/connect)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

{% tabs %}

{% tab title="npm" %}
```bash
npm install @wanderapp/connect
```
{% endtab %}

{% tab title="yarn" %}
```bash
yarn add @wanderapp/connect
```
{% endtab %}

{% tab title="pnpm" %}
```bash
pnpm add @wanderapp/connect
```
{% endtab %}

{% tab title="bun" %}
```bash
bun add @wanderapp/connect
```
{% endtab %}

{% endtabs %}

## Basic Usage

To use the Wander Connect embedded wallet, you first need to instante it:

```javascript
import { WanderConnect } from "@wanderapp/connect";

// Initialize Wander Connect:
const wander = new WanderConnect({ clientId: "FREE_TRIAL" });
```

{% hint style="warning" %}
Wander Connect will not require a developer account on launch. You can start using it with `clientId: "FREE_TRIAL"`.

However, we'll soon require developers to sign up for a developer account, where you'll get your own `clientId` and get access new customization options.
{% endhint %}

After this, the default Wander Connect button will appear fixed in the bottom-right corner of the screen:

TODO: Add screenshot.

Clicking it will open a popup where your users can authenticate:

TODO: Add screenshot.

And, once authenticated, the default wallet UI will appear, again, fixed in the bottom-right corner of the screen:

TODO: Add screenshot.

Once the user authenticates, you should request permissions using [`connect()`](api/connect.md). This will prompt your
users to connect their wallet to your dApp:

TODO: Add screenshot.

You can use the `onAuth` option to listen for authentication changes, and request permissions to connect to the wallet
just after the user authenticates. After they accept, your dApp can start interacting with the wallet:

TODO: Update to use `arweaveWalletLoaded` event.

```typescript
import { WanderConnect } from "@wanderapp/connect";

// Initialize Wander Connect:
const wander = new WanderConnect({
  clientId: "FREE_TRIAL",
  onAuth: (userDetails) => {
    if (!!userDetails) {
      try {
        // 1. Connect your app to the wallet:
        await arweaveWallet.connect([...]);

        // 2. Create Arweave transaction:
        const tx = await arweave.createTransaction({ ... });

        // 3. Sign transaction:
        await arweave.transactions.sign(tx);

        // 4. TODO: Handle (e.g. post) signed transaction...

      } catch () {
        alert("The wallet wasn't connected.")
      }
    }
  }
});

```

Depending on what type of access the user granted, they'll be prompted again to sign the transaction:

TODO: Add screenshot.

{% hint style="info" %}
As you can see in the example above, to use Wander Connect in your application, you don't need to integrate or learn how most of the [Wander Injected API](api/intro) works. Using [`arweave-js`](https://npmjs.com/arweave), you can easily sign a transaction through Wander Connect.

However, note that the [Wander Injected API](api/intro) is exactly the same for both Wander Connect and the Wander Browser Extension, and can be accessed at `window.arweaveWallet` after instantiating Wander Connect.
{% endhint %}

Additional features and options, only available for Wander Connect (not available for the Wander Browser Extension), are available through the SDK options, methods and callbacks:

// TODO: Replace with Cards: https://docs.gitbook.com/creating-content/blocks/cards

{% content-ref url="connect/options" %} . {% endcontent-ref %}

{% content-ref url="connect/methods" %} . {% endcontent-ref %}

{% content-ref url="connect/callbacks" %} . {% endcontent-ref %}

### React

When using React, the example above stays mostly the same. The main change needed is to add a `useEffect` block to run
it, and, optionally, a [Ref](https://react.dev/learn/referencing-values-with-refs) to keep a reference to the
`WanderConnect` instance you've just created:;

```typescript
import { useRef, useState } from "react";
import { WanderConnect } from "@wanderapp/connect";

export function MyApp() {
  const wanderRef = useRef(null);

  useEffect(() => {
    // Initialize Wander Connect:
    const wander = new WanderConnect({
      clientId: "FREE_TRIAL",
      onAuth: (userDetails) => {
        if (!!userDetails) {
          try {
            // 1. Connect your app to the wallet:
            await arweaveWallet.connect([...]);

            // 2. Create Arweave transaction:
            const tx = await arweave.createTransaction({ ... });

            // 3. Sign transaction:
            await arweave.transactions.sign(tx);

            // 4. TODO: Handle (e.g. post) signed transaction...

          } catch () {
            alert("The wallet wasn't connected.")
          }
        }
      }
    });

    // Keep a reference to the instance:
    wanderRef.current = wander;

    // Clean up on unmount:
    return () => {
      wanderRef.current = null;
      wander?.destroy();
    };
  }, []);

  return ...;
}
```

### Next.js

To use Wander Connect on a Next.js site, you would follow the same steps describe above in the React section. However,
if you are using the App Router, you need to make sure you load Wander Connect in a client component.

## Customization

Wander Connect supports 4 types of layout plus light and dark themes, which should be enough for most projects. If you
need to better match your brand and app look and feel, Wander Connect also includes various advanced customization
options, but if that's still not enough, you can always opt-out of the default UI and provide a custom one:

// TODO: Replace with Cards: https://docs.gitbook.com/creating-content/blocks/cards

{% content-ref url="connect/options" %} . {% endcontent-ref %}

{% content-ref url="connect/advanced-customization" %} . {% endcontent-ref %}

{% content-ref url="connect/custom-ui" %} . {% endcontent-ref %}

## Architecture & Security

Wander Connect uses [Shamir Secret Sharing](https://en.wikipedia.org/wiki/Shamir%27s_secret_sharing) to split users'
private keys in 2 shares, one stored in the users' device and one stored in our servers.

In order for users to use one of their private keys, they need to authenticate and prove they have the corresponding
(device) share, without actually transferring it to our servers (so that users' private keys never reach our servers).
Once they do that, the server will send back its share, and the Wander Connect app running in the user's device will
reconstruct the private key.

We use [Privy's `shamir-secret-sharing`](https://www.npmjs.com/package/shamir-secret-sharing) package, which has been
audited and is actively maintained.

## Browser Support

The SDK supports all modern browsers (Chrome, Firefox, Safari, Edge).
