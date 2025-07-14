---
description: Methods available on the Wander Connect SDK
---

# Methods

## `open(directAccess?: DirectAccess)`&#x20;

Opens the wallet interface, in a specific flow/page, if specified.

## `close()`&#x20;

Closes the wallet interface.

## `signOut()`&#x20;

Signs out the user.

## `setTheme(theme: ThemeSetting)`&#x20;

Update the app, iframe and button themes.

Note that if `options.iframe.theme` or `options.button.theme` are used, the iframe theme and/or the button theme, respectively, won't be updated. In that case, you should call `setIframeTheme()` and/or `setButtonTheme()`.

## `setIframeTheme(theme: ThemeSetting)`&#x20;

Update the iframe theme (outside only, doesn't affect the iframe content's / app theme).

## `setButtonTheme(theme: ThemeSetting)`&#x20;

Update the button theme.

## `destroy()`&#x20;

Removes all elements and event listeners.
