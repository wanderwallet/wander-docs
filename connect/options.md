---
description: Options for the Wander Connect SDK
---

# Wander Connect Options

The Wander Connect SDK allows you customize the 2 different UI components it renders on the screen: the iframe and
the button:

```javascript
import { WanderEmbedded } from "@wanderapp/embed-sdk";

// Initialize Wander Connect:
const wander = new WanderConnect({
  clientId: "ALPHA",
  iframe: {
    layout: {
      type: "popup",
      position: "bottom-right",
    }
  },
  button: {
    position: "bottom-right",
    label: true,
  }
});
```

## Wallet Customization Options

```typescript
interface WanderEmbeddedComponentOptions {
  id?: string;
  theme?: ThemeSetting;
  cssVars?: Partial<T> | Partial<Record<ThemeVariant, Partial<T>>>;
  customStyles?: string;
  routeLayout?:
    | LayoutType
    | LayoutConfig
    | Partial<Record<RouteType, LayoutType | LayoutConfig>>;
  clickOutsideBehavior?: boolean;
}
```

TODO: Add link to GitHub.




## Button Customization Options

```typescript
interface WanderEmbeddedComponentOptions {
  id?: string;
  theme?: ThemeSetting;
  cssVars?: Partial<T> | Partial<Record<ThemeVariant, Partial<T>>>;
  customStyles?: string;
  parent?: HTMLElement;
  position?: WanderEmbeddedButtonPosition;
  wanderLogo?: WanderEmbeddedLogoVariant;
  dappLogoSrc?: string; // TODO: Remove?
  label?: boolean;
  balance?: boolean | WanderEmbeddedBalanceOptions;
  notifications?: WanderEmbeddedButtonNotifications;
  i18n?: WanderEmbeddedButtonLabels;
}
```

TODO: Add link to GitHub.
