---
description: ArConnect Injected API `connect()` function
---

# 🔗 Connect

To use the different functionalities the ArConnect API provides, you need to request permissions from the user to interact with their wallets. Each API function has their own permission, which can be requested at any time with the `connect()` function.

| Argument      | Type                 | Description                                     |
|---------------|----------------------|-------------------------------------------------|
| `permissions` | `PermissionType[]`   | An array of permission to request from the user |
| `appInfo`     | `AppInfo` (optional) | Additional information about the app            |
| `gateway`     | `Gateway` (optional) | Custom gateway config                           |
