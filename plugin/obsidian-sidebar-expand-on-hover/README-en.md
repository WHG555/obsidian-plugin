## Obsidian Sidebar Expand on Hover Plugin

### Features

- Expand sidebars on mouse hovering on the corresponding ribbons.
- Pin/unpin sidebar state(expand/collapse) by double clicking on the ribbons.
- Set sidebar width either by dragging or setting the value in plugin settings.
- Keep previous state of sidebars on relaunch.

### Demo:

![Plugin in Action: Auto expand of sidebar when hovering on ribbon](demo.gif)

### TODO:

- [ ] Option to toggle sidebar animations.
- [ ] Change animation style.

### How to Install (Manual):

- If Obsidian is running then close it.
- Locate your Obsidian vault. (It's where you keep your notes)
- Run the following commands in terminal:
  ```bash
  $ cd <vault>/.obsidian/plugins/
  $ git clone https://github.com/toiq/obsidian-sidebar-expand-on-hover
  ```
- Now launch Obsidian and go to `settings > Community Plugins > Installed Plugins` and enable this plugin. (Make sure you disabled 'Safe Mode')

### How to Uninstall:

- go to `settings > Community Plugins > Installed Plugins` and click the X besides this plugin's name.
- Restart Obsidian.
