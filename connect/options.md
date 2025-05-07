---
description: Options for the Wander Connect SDK
---

# Wander Connect Options

The Wander Connect SDK options include:

- SDK setup options.
- Basic customization options.
- Specific customization options for the 2 different UI components it renders on the screen: the iframe and the button.
- Event callbacks.

A more complete example will look something like this:

```javascript
import { WanderEmbedded } from "@wanderapp/embed-sdk";

// Initialize Wander Connect:
const wander = new WanderConnect({
  clientId: "FREE_TRIAL",
  theme: "dark",
  iframe: {
    layout: {
      type: "popup",
      position: "bottom-left",
    }
  },
  button: {
    position: "bottom-left",
    label: true,
  },
  onAuth: () => handleAuth,
});
```

###### API 

```typescript
interface IframeOptions {
  clientId: string;
  theme?: ThemeSetting;
  hideBE?: boolean;
  baseURL?: string;
  baseServerURL?: string;
  iframe?: IframeOptions | HTMLIFrameElement;
  button?: ButtonOptions | boolean;
  onAuth?: (authInfo: AuthInfo) => void;
  onOpen?: () => void;
  onClose?: () => void;
  onResize?: (routeConfig: RouteConfig) => void;
  onBalance?: (balanceInfo: BalanceInfo) => void;
  onRequest?: (requestsInfo: RequestsInfo) => void;

}
```

## Iframe Customization Options

### Iframe Layout

```javascript
const wander = new WanderConnect({
  iframe: {
    routeLayout: {
      // Different layouts for different routes
      default: {
        type: "popup",
        position: "bottom-right",
      },
      auth: {
        type: "modal",
      },
      "auth-request": {
        type: "sidebar",
        position: "right",
        expanded: true,
      },
    },
    cssVars: {
      background: "#f5f5f5",
      borderRadius: 12,
      boxShadow: "0 8px 32px rgba(0, 0, 0, 0.12)",
    },
  },
});
```

###### API 

```typescript
interface IframeOptions {
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


### Button Positioning

You have three methods for custom positioning:


#### Using Predefined Positions

```javascript
const wander = new WanderConnect({
  button: {
    position: "bottom-right", // Options: "bottom-right", "bottom-left", "top-right", "top-left"
  },
});
```

#### Using a Parent Element

First, create a container element:

```html
<div id="wanderButtonContainer"></div>
```

Then reference it in your configuration:

```javascript
const wander = new WanderConnect({
  button: {
    position: "static",
    parent: document.getElementById("wanderButtonContainer"),
  },
});
```

#### Using Custom Styles

```javascript
const wander = new WanderConnect({
  button: {
    position: "static",
    // Using customStyles for precise control over button appearance and position
    customStyles: `
      /* Position the button container */
      :host {
        position: fixed;
        top: 20px;
        right: 20px;
      }

      /* Style the button itself */
      .button {
        background: rgba(255, 255, 255, 0.9);
        backdrop-filter: blur(8px);
      }
    `,
  },
});
```

#### Using External CSS

Define the button with a custom ID:

```javascript
const wander = new WanderConnect({
  button: {
    position: "static",
    id: "my-wander-button", // Default is "wanderEmbeddedButtonHost"
  },
});
```

Then style it with external CSS:

```css
/* Position the button container */
#my-wander-button {
  position: fixed;
  top: 20px;
  right: 20px;
}
```

###### API 

```typescript
interface ButtonOptions {
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
