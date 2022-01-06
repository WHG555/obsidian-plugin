[![GitHub tag (Latest by date)](https://img.shields.io/github/v/tag/mcndt/obsidian-toggl-integration)](https://github.com/mcndt/obsidian-toggl-integration/releases) ![GitHub all releases](https://img.shields.io/github/downloads/mcndt/obsidian-toggl-integration/total)
# Toggl Track Integration for Obsidian
Add integration with the Toggl Track API to manage your timers inside Obsidian.

## Functionality
- See your current timer and how long it has been running  in the status bar
- Get a summary of your day in the side panel
- Create and start a new timer using the command palette, or restart an recent one
- Stop your timer using the command palette

![](demo.gif)

## Setup
Configuring this plugin requires you to first request an API token from Toggl. More info on how to do this [can be found here](https://support.toggl.com/en/articles/3116844-where-is-my-api-token-located).

To set up this plugin, simply enter your API token in the settings tab, click connect and select the Toggl Workspace you wish to use.

![settings](settings.png)

## Use with other plugins:

### QuickAdd

The developer of the QuickAdd plugin has created a preset menu for timers using QuickAdd. You can find out how he did it on the Obsidian Discord server ([link to message](https://discord.com/channels/686053708261228577/707816848615407697/876069796553293835)).

## Roadmap

You can see my more detailed roadmap for this plugin on this page: [Development Roadmap](https://github.com/mcndt/obsidian-toggl-integration/projects/1). I try to keep the cards in each column sorted by priority.

## Feature Requests
Please make feature requests in the GitHub discussions tab: [click here](https://github.com/mcndt/obsidian-toggl-integration/discussions/categories/feature-requests)

If you would to like to talk about the plugin with me more directly, you can find me in the Obsidian Discord server as `Maximio#6460`. Feel free to tag me!

## Dependencies
Currently I rely on this repo for providing a JavaScript interface with the Toggl Track API: https://github.com/saintedlama/toggl-client

However in the future I might write fork this so I can refactor it to use mobile friendly APIs (e.g. using Obsidian’s own request API).

## Support
If you like this plugin and want to support me, you can do so via *Buy me a Coffee*:

<a href="https://www.buymeacoffee.com/mcndt"><img src="https://img.buymeacoffee.com/button-api/?text=Buy me a coffee&emoji=&slug=mcndt&button_colour=5F7FFF&font_colour=ffffff&font_family=Inter&outline_colour=000000&coffee_colour=FFDD00"></a>
