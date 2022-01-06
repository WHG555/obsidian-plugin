# Open in VSCode

This plugin for [Obsidian](https://obsidian.md/) makes a ribbon button and a command to open your vault as a Visual Studio Code workspace.

You can use VSCode for various purposes with your vault, such as for git version control, markdown formatting with [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode), linting with [markdownlint](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint), [mass formatting files](https://marketplace.visualstudio.com/items?itemName=jbockle.jbockle-format-files) and more.

![video showcase](125867690-c11f4396-e31b-4232-9ea5-822bf729df9a.gif)

The icons work with light and dark mode.

![light and dark](125868293-96c6f541-0604-4238-9fc3-05ff6c2e08df.gif)

You can also use it as a command and assign hotkeys to it. You can disable the ribbon button in settings.
![command](125869408-d39d870b-ab4f-42d0-b915-b6abc1e617d5.png)

By default the plugin uses `child_process` to launch VSCode with the `code` command, but the previous method using URLs can still be enabled.

You can template the command opening VSCode however you like with its [provided command line arguments](https://code.visualstudio.com/docs/editor/command-line). This way you can technically launch any command you set, so take caution. Potential use cases include opening workspaces with `.code-workspace` files (e.g. for Dendron), opening specific files, folders, etc.

## Compatibility

The plugin was tested in Obsidian v0.11.13 and subsequent versions, but probably works with older versions.

## Installation

You can install the plugin via the Community Plugins tab within Obsidian.
You can also manually copy from releases to your `.obsidian/plugins/open-vscode` folder.

## Issues

Using the URL method for opening, VSCode can't open a workspace without a further confirmation dialog (that you just can hit enter on) for security reasons. See [this issue](https://github.com/microsoft/vscode/issues/95670) for more infomation.

## Credits

Toggle ribbon setting by [@ozntel](https://github.com/ozntel).

Thank you to the makers of the [DEVONlink](https://github.com/ryanjamurphy/DEVONlink-obsidian) plugin, as it was a great starting point for working with ribbon icons in Obsidian.
The icon is from [icon-icons.com](https://icon-icons.com/icon/visual-studio-code-logo/144754) and was resized with [iLoveIMG](https://www.iloveimg.com/resize-image/resize-svg).

## Support

If you like this plugin you can support me on PayPal here: [![Paypal](https://img.shields.io/badge/paypal-nomarcub-yellow?style=social&logo=paypal)](https://paypal.me/nomarcub)
