---
description: Custom UI for the Wander Connect Embedded Wallet
---

# Custom UI

If the [Advanced Customization Options](advanced-customization.md) provided by the Wander Connect SDK are not\
enough for your, you can instead provide your own `iframe` element (reference) and use the[SDK methods](methods.md) to open/closing the wallet without relaying on the default injected button.

## Providing a custom `iframe`

```javascript
const wander = new WanderConnect({
  iframe: document.getElementById("wander-iframe"),
});
```

## Disabling the default injected `button`

```javascript
const wander = new WanderConnect({
  button: false,
});
```
