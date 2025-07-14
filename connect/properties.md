---
description: Properties for the Wander Connect SDK
---

# Properties

## `authInfo: AuthInfo`&#x20;

Contains the current authentication state of the SDK, and it is initialized with cached data in order to show as soon as possible the non-auth or the loading auth UIs.

## `routeConfig: RouteConfig | null`&#x20;

Current route configuration including dimensions and layout preferences.

## `backupInfo: BackupInfo | null`

User's current backup information.

## `balanceInfo: BalanceInfo | null`&#x20;

User's current balance information.

## `pendingRequests: number`&#x20;

Number of pending requests awaiting user action.

## `isOpen: boolean`

Indicates whether the wallet interface is currently open/visible.

## `width: number | undefined`

Current width of the wallet interface in pixels.

## `height: number | undefined`&#x20;

Current height of the wallet interface in pixels.

