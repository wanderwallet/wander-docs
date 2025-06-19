---
description: Methods available on the Wander Connect SDK
---

# Methods

* `open()` - Opens the wallet interface.
* `close()` - Closes the wallet interface.
* `signOut()` - Signs out the user.
* `setTheme(theme: ThemeSetting)`  - Update the app, iframe and button themes. Note that if `options.iframe.theme` or `options.button.theme` were used, the iframe theme and/or the button theme, respectively, won't be updated. In that case, you should call `setIframeTheme()` and/or `setButtonTheme()`.
* `setIframeTheme(theme: ThemeSetting)`  - Update the iframe theme (outside only, doesn't affect the iframe content's / app theme).
* `setButtonTheme(theme: ThemeSetting)`  - Update the button theme.
* `destroy()` - Removes all elements and event listeners.
