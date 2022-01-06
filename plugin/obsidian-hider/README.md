Support the development of my plugins and themes **@kepano** on [Twitter](https://www.twitter.com/kepano), [Patreon](https://www.patreon.com/kepano) or [Buy me a coffee](https://www.buymeacoffee.com/kepano).

<a href="https://www.buymeacoffee.com/kepano"><img src="https://img.buymeacoffee.com/button-api/?text=Buy me a coffee&emoji=&slug=kepano&button_colour=5F7FFF&font_colour=ffffff&font_family=Poppins&outline_colour=000000&coffee_colour=FFDD00"></a>

## Overview

This plugin enables you to hide certain parts of the Obsidian UI. Note that your CSS theme may override Hider.

- Hide app ribbon (can be bound to a hotkey)
- Hide status bar (can be bound to a hotkey)
- Hide title bar
- Hide scrollbars
- Hide tooltips
- Hide instructions in prompts

## Making your theme compatible with Hider

Hider injects the following classes on the `body` element when features are toggled on.

| Toggle | Class |
| ------ | ----- |
| Title bar | `.hider-frameless` |
| App ribbon | `.hider-ribbon` |
| Status bar | `.hider-status` |
| Scrollbars | `.hider-scroll` |
| Tooltips | `.hider-tooltips` |
| Instructions | `.hider-instructions` |
