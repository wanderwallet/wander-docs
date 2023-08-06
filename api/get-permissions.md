---
description: ArConnect Injected API getPermissions() function
---

# Retrive permissions

As discussed [here](connect.md#permissions), ArConnect requires a specific type of permission for each API function that involves an action with the user's wallet. It is important for an application to be aware of the permissions given to them by the user. The `getPermissions()` function returns an array of permissions given to the current application. If the array is empty, it means that the app has not yet connected to the extension.

## Example usage

```ts
// get permissions
const permissions = await window.arweaveWallet.getPermissions();

console.log("The app has the following permissions:", permissions);
```
