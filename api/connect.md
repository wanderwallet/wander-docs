---
description: ArConnect Injected API connect() function
---

# Connect

To use the different functionalities the ArConnect API provides, you need to request permissions from the user to interact with their wallets. Each API function has their own permission(s), which can be requested at any time with the `connect()` function.

| Argument      | Type                                                       | Description                                                                       |
| ------------- | ---------------------------------------------------------- | --------------------------------------------------------------------------------- |
| `permissions` | [`Array<PermissionType>`](connect.md#permissions)          | An array of permission to request from the user (at least one has to be included) |
| `appInfo?`    | [`AppInfo`](connect.md#additional-application-information) | Additional information about the app                                              |
| `gateway?`    | [`Gateway`](connect.md#custom-gateway-config)              | Custom gateway config                                                             |

{% hint style="info" %}
**Note:** The `appInfo` argument is optional, if it is not provided, the extension will use your site's title and favicon as application data.
{% endhint %}

{% hint style="info" %}
**Note:** The `gateway` argument is optional, if it is not provided, the extension will use the default `arweave.net` gateway for the executed API. functions
{% endhint %}

## Permissions

ArConnect requires specific permissions from the user for each interaction that involves the usage of their wallet.

| Permission              | Description                                                             |
| ----------------------- | ----------------------------------------------------------------------- |
| `ACCESS_ADDRESS`        | Allow the app to get the active wallet's address                        |
| `ACCESS_PUBLIC_KEY`     | Enable the app to access the active wallet's public key                 |
| `ACCESS_ALL_ADDRESSES`  | Enable the app to access the active wallet's public key                 |
| `SIGN_TRANSACTION`      | Allow the app to sign an Arweave transaction (Base layer)               |
| `ENCRYPT`               | Enable the app to encrypt data with the user's wallet through ArConnect |
| `DECRYPT`               | Allow the app to decrypt data encrypted with the user's wallet          |
| `SIGNATURE`             | Allow the app to sign messages with the user's wallet through ArConnect |
| `ACCESS_ARWEAVE_CONFIG` | Enable the app to access the current gateway config                     |
| `DISPATCH`              | Allow the app to dispatch a transaction (bundle or base layer)          |

## Additional application information

You can provide your application's name and logo to the extension. Please make sure the app name only includes the **name of your application** and the logo is **high quality** and clearly visible on dark and light backgrounds.

```ts
interface AppInfo {
  name?: string; // optional application name
  logo?: string; // optional application logo url
}
```

## Custom gateway config

If your application requires the usage of a special gateway or you want to test with an [ArLocal](https://github.com/textury/arlocal) testnet gateway, you'll have to provide some information about these when connecting to ArConnect.

```ts
interface Gateway {
  host: string;
  port: number;
  protocol: "http" | "https";
}
```

## Example usage

```ts
// connect to the extension
await window.arweaveWallet.connect(
  // request permissions to read the active address
  ["ACCESS_ADDRESS"],
  // provide some extra info for our app
  {
    name: "Super Cool App",
    logo: "https://arweave.net/jAvd7Z1CBd8gVF2D6ESj7SMCCUYxDX_z3vpp5aHdaYk"
  },
  // custom gateway
  {
    host: "g8way.io",
    port: 443,
    protocol: "https"
  }
);
```
