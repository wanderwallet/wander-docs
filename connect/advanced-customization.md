---
description: Advanced customization options for the Wander Connect Embedded Wallet
---

# Wander Connect Advanced Customization

The Wander Connect SDK allows you customize different CSS variables for the 2 different UI components it renders on the
screen: the wallet and the button. Additionally, you can also inject your own custom CSS.

## Customize CSS Variables

### Iframe

```javascript
const wander = new WanderConnect({
  iframe: {
    cssVars: {
      background: "#f5f5f5",
      borderRadius: 12,
      boxShadow: "0 8px 32px rgba(0, 0, 0, 0.12)",
    },
  },
});
```

### Button

```javascript
const wander = new WanderConnect({
  button: {
    position: "top-right",
    cssVars: {
      // Light theme variables
      light: {
        background: "#ffffff",
        color: "#000000",
        borderRadius: 16,
        boxShadow: "0 4px 12px rgba(0, 0, 0, 0.1)",
      },
      // Dark theme variables
      dark: {
        background: "#1a1a1a",
        color: "#ffffff",
        borderRadius: 16,
        boxShadow: "0 4px 12px rgba(0, 0, 0, 0.3)",
      },
    },
  },
});
```

## Inject custom CSS

### Iframe

You can add custom CSS styles to the iframe using `customStyles` option. When using this option, you must use CSS
selectors to target specific elements.

Available selectors:

- `.backdrop` - Targets the backdrop overlay behind the iframe
  - `.backdrop.show` - Applied when the backdrop is visible
- `.iframe-wrapper` - Targets the container that wraps the iframe
  - `.iframe-wrapper.show` - Applied when the iframe is visible
- `.iframe` - Targets the actual iframe element
- `.half-image` - Targets the image element used in half layout mode
  - `.half-image.show` - Applied when the half-image is visible

The HTML structure is follows:

```html
<div class="wrapper">
  <iframe class="iframe"></iframe>
</div>
<div class="backdrop"></div>
<div class="half-image"></div>
```

Example usage:

```javascript
const wander = new WanderConnect({
  iframe: {
    customStyles: `
      /* Style the backdrop */
      .backdrop {
        background: rgba(0, 0, 0, 0.5);
        backdrop-filter: blur(8px);
        transition: opacity 200ms ease;
      }

      .backdrop.show {
        opacity: 1;
      }

      /* Style the iframe wrapper */
      .iframe-wrapper {
        border: none;
        border-radius: 16px;
        box-shadow: 0 8px 32px rgba(0, 0, 0, 0.2);
        transition: transform 200ms ease, opacity 200ms ease;
      }

      .iframe-wrapper.show {
        opacity: 1;
        transform: none;
      }

      /* Style the iframe itself */
      .iframe {
        border-radius: inherit;
        background: white;
      }

      /* Style the half-image */
      .half-image {
        object-fit: cover;
        transition: opacity 300ms ease;
      }

      .half-image.show {
        opacity: 1;
      }

      /* Mobile-specific styles */
      @media (max-width: 540px) {
        .backdrop {
          backdrop-filter: none;
        }

        .iframe-wrapper {
          border-radius: 0;
        }
      }
    `,
  },
});
```

The iframe wrapper element (`.iframe-wrapper`) has several data attributes that you can use for conditional styling:

- `[data-layout="popup|modal|sidebar|half"]` - Current layout type
- `[data-position="left|right|top-left|top-right|bottom-left|bottom-right"]` - Position of the iframe
- `[data-expanded="true|false"]` - Whether the iframe is in expanded mode
- `[data-expand-on-mobile="true|false"]` - Whether the iframe expands on mobile devices

You can also use these when targeting the iframe element (`.iframe`):

```css
.iframe-wrapper[data-layout="popup"] > .iframe {
  ...;
}
```

Or the backdrop element (`.backdrop`):

```css
.iframe-wrapper[data-layout="popup"] + .backdrop {
  ...;
}
```

You can use these attributes in your `customStyles` to style different states:

```javascript
customStyles: `
  /* Style popup layout */
  .iframe-wrapper[data-layout="popup"] {
    transform: scale(0.95);
  }

  .iframe-wrapper[data-layout="popup"].show {
    transform: scale(1);
  }

  /* Style expanded sidebar */
  .iframe-wrapper[data-layout="sidebar"][data-expanded="true"] {
    border: none;
    border-radius: 0;
  }

  /* Style right-positioned half layout */
  .iframe-wrapper[data-layout="half"][data-position="right"] {
    border-left: 2px solid rgba(0, 0, 0, 0.1);
  }

  /* Style mobile expanded state */
  .iframe-wrapper[data-expand-on-mobile="true"] {
    width: 100vw;
    height: 100vh;
    border: none;
    border-radius: 0;
  }

  /* Combine attributes for specific cases */
  .iframe-wrapper[data-layout="sidebar"][data-position="right"][data-expanded="true"] {
    box-shadow: -8px 0 32px rgba(0, 0, 0, 0.1);
  }
`;
```

### Button

You can add custom CSS styles to the button using `customStyles` option. When using this option, you must use CSS
selectors to target specific elements.

Available selectors:

- `:host` - Targets the button container
- `.button` - Targets the button element
- `.wanderLogo` - Targets the Wander logo SVG
- `.label` - Targets the button text label
- `.balance` - Targets the balance display
- `.indicator` - Targets the connection status indicator
- `.notifications` - Targets the notifications badge

Example usage:

```javascript
const wander = new WanderConnect({
  button: {
    customStyles: `
      /* Position the button container */
      :host {
        position: fixed;
        top: 20px;
        right: 20px;
      }

      /* Target the button element */
      .button {
        width: 200px;
        display: flex;
        align-items: center;
        justify-content: center;
      }

      /* Target the Wander logo */
      .wanderLogo {
        width: 24px;
        height: 24px;
      }

      /* Target the button label */
      .label {
        font-size: 14px;
        font-weight: 500;
      }

      /* Target the balance display */
      .balance {
        font-size: 12px;
        opacity: 0.8;
      }

      /* Target the connection indicator */
      .indicator {
        width: 6px;
        height: 6px;
      }

      /* Target the notifications badge */
      .notifications {
        font-size: 10px;
        padding: 2px 6px;
      }
    `,
  },
});
```

The button element has a `data-variant` HTML attribute you can use for styling:

- `[data-variant="loading|onboarding|authenticated|not-authenticated"]`

As well as some CSS classes that are added based on its state:

- `.isConnected` - Added when the wallet is connected
- `.isOpen` - Added when the wallet interface is open

Additionally, the button's `.label` and `.balance` elements also have some modifiers:

- `.label.isLoading`
- `.balance.isLoading`
- `.balance.isHidden`

You can use these classes in your `customStyles` to style different states:

```javascript
customStyles: `
  .button.isAuthenticated {
    border-color: green;
  }

  .button.isConnected {
    background: rgba(0, 255, 0, 0.1);
  }

  .button.isOpen {
    transform: scale(0.95);
  }
`;
```
