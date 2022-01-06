# Obsidian Vimrc Support Plugin

This plugin loads a file of Vim commands from `VAULT_ROOT/.obsidian.vimrc`.
For users of the Obsidian.md Vim mode, this is very useful for making various settings (most notably keymaps) persist.

Note that this plugin is **not** the Vim support of Obsidian -- that support is built-in and you can perfectly use Obsidian in Vim mode without this plugin.
This plugin merely implements the ability to load a persistent configuration and adds a few extras.

## Usage

First and foremost, make sure you have the Obsidian Vim key bindings turned on -- see Editor -> Vim key bindings.

Now to keep some of your Vim settings permanent, install this plugin and put a file named `.obsidian.vimrc` in your vault root.
If you're using multiple vaults, you'll need this file on each one.

Here's a simple & useful `.obsidian.vimrc` that I'm using:

```
" Have j and k navigate visual lines rather than logical ones
nmap j gj
nmap k gk
" I like using H and L for beginning/end of line
nmap H ^
nmap L $
" Quickly remove search highlights
nmap <F9> :nohl

" Yank to system clipboard
set clipboard=unnamed

" Go back and forward with Ctrl+O and Ctrl+I
" (make sure to remove default Obsidian shortcuts for these to work)
exmap back obcommand app:go-back
nmap <C-o> :back
exmap forward obcommand app:go-forward
nmap <C-i> :forward
```

## Supported Commands

The commands that can be used are whatever CodeMirror supports.
I couldn't find a formal list anywhere but you can look for `defaultExCommandMap` in [the source code](https://github.com/codemirror/CodeMirror/blob/master/keymap/vim.js), or play around with trying commands in Obsidian's Vim mode.

In addition to that:
- The plugin skips blank lines and lines starting with Vimscript comments (`" ...`).
- Special support for yanking to system clipboard can be activated by `set clipboard=unnamed` (`unnamedplus` will do the same thing).
- Support for the `tabstop` Vim option (e.g. `set tabstop=4`).
- Custom mapping/unmapping commands in addition to the defaults: `noremap` and `iunmap` (PRs are welcome to implement more :) )
- `exmap [commandName] [command...]`: a command to map Ex commands. This should basically be supported in regular `:map`, but doesn't work with multi-argument commands due to a CodeMirror bug, so this is a workaround.
- `obcommand` - execute Obsidian commands, see more details below.
- `surround` - surround your selected text in visual mode or word in normal mode with text.
- `pasteinto` - paste your current clipboard into your selected text in visual mode or word in normal mode. Useful for creating hyperlinks.

Commands that fail don't generate any visible error for now.

**Important tip!** Before adding commands to your Vimrc file, you should try them in Obsidian's normal mode (type '`:`' in the editor) to make sure they work as expected.
CodeMirror's Vim mode has some limitations and bugs and not all commands will work like you'd expect.
In some cases you can find workarounds by experimenting, and the easiest way to do that is by trying interactively rather than via the Vimrc file.

## Installation

In the Obsidian.md settings under "Third-party plugin", turn off Safe mode, then browse to this plugin.

Alternatively (and less recommended), you can install it manually: just copy `main.js` and `manifest.json` to your vault `VaultFolder/.obsidian/plugins/obsidian-vimrc-support/`.

## "Please implement \[some Vim feature here\]..."

I'd like to emphasize again that this plugin is a tweak to Obsidian's built-in Vim mode, which is in turn mostly the [Vim mode of CodeMirror](https://codemirror.net/demo/vim.html). And while I am personally very fond of helping everybody make use of Vim modes everywhere, this plugin is often not the best place to implement some types of features.

1. Vim editor features (e.g. new motions) would best be implemented in CodeMirror, so other editors using this component would enjoy them too! Please consider submitting issues or pull requests [there](https://github.com/codemirror/CodeMirror/) first.
2. Features that are already implemented by other Obsidian plugins are best to stay in these plugins. Please consider asking these plugin authors to add Vim support for their features (using the CodeMirror API), or even better -- help them out :)

Having said that, adding features here in this plugin is often very easy thanks to the CodeMirror [API for extending its Vim mode](https://codemirror.net/doc/manual.html#vimapi_extending), so as the path of least resistance I will occassionally implement some requested Vim features and be happy to accept PRs.

Things I'd love to add:
- Implement some standard `vim-markdown` motions for Obsidian, e.g. `[[`, or implement for CodeMirror the 1-2 missing Ex commands required to define these keymaps in the Vimrc.
- Relative line numbers.

## Change Vimrc File Location/Name

If you want the Vimrc file name or path to be different than the default, there is a plugin setting (under Settings | Plugin Options | Vimrc Support) to change that.

## Executing Obsidian Commands with `obcommand`

The plugin defines a custom Ex command named `obcommand` to execute various Obsidian commands as an Ex command.
This is useful to map external functionality of Obsidian or other plugins to Vim shortcuts, but it's not as easy to use as one would hope.

If you just type `:obcommand` you'll get in the Developer Console (Ctrl+Shift+I) the list of commands that are currently defined by the app.
The simple syntax `:obcommand [commandName]` will execute the named command.

Some useful examples:
- `obcommand editor:insert-link`
- `obcommand editor:toggle-comment`
- `obcommand app:go-back`
- `obcommand workspace:split-vertical`

And many more.

**WARNING:** this is not a formal API that Obsidian provides and is done in a rather hacky manner.
It's definitely possible that some future version of Obsidian will break this functionality.

## Surround Text with `surround`

The plugin defines a custom Ex command named `surround` to surround either your currently selected text in visual mode or the word your cursor is over in normal mode with text.
This is particularly useful for creating wikilinks in Obsidian `[[WikiLink]]`.

The syntax follows `:surround [prefixText] [postfixText]`.

Some examples:
- `surround ( )`
- `surround [[ ]]`

Here's my surround config as an example:

```
" Surround text with [[ ]] to make a wikilink
" NOTE: must use 'map' and not 'nmap'
exmap wiki surround [[ ]]
map [[ :wiki
```

## Inserting Links/Hyperlinks with `pasteinto`

The plugin defines a custom Ex command named `pasteinto` to paste text into your currently selected text in visual mode, or the word your cursor is over in normal mode.
This is particularly useful for creating links/hyperlinks `[selected-text](paste)`.

Here's my hyperlink config as an example:
```
" Maps pasteinto to Alt-p
map <A-p> :pasteinto
```

### Mapping Obsidian Commands Within Vim

Next thing you probably wanna ask is "how do I map the great Obsidian commands to Vim commands?"

The trivial answer should have been something along the line of `:nmap <C-o> :obcommand app:go-back`, but this **does not work** because of an annoying CodeMirror bug.
Turns out that the various mapping commands of CodeMirror pass only the first argument, so when you execute your mapping if defined as above, `:obcommand` would execute with no arguments.

Here comes a custom command to the rescue, `exmap`, which you can use to "alias" Ex commands for longer Ex commands: `:exmap back obcommand app:go-back`.
You now have a simple (0 argument) Ex command named `back` that goes back in Obsidian, and *that* is something you can map.

To summarize, here's how you map `C-o` to Back:
```
exmap back obcommand app:go-back
nmap <C-o> :back
```

Note how `exmap` lists command names without colons and in `nmap` the colon is required.

## Some Help with Binding Space Chords (Doom and Spacemacs fans)

`<Space>` can be bound to make chords, such as `<Space>fs` in conjunction with obcommand to save your current file and more.
But first `<Space>` must be unbound with `unmap <Space>`.
Afterwards `<Space>` can be mapped normally as any other key.

## Fixed Keyboard Layout in Normal Mode

In many languages and keyboard layouts it becomes problematic or plain impossible to use Vim keys.
The Vim keys are located in different positions on some keyboard layouts, which could be confusing when switching
layouts, and on some layouts (e.g. non-Western languages) the keys for Vim movements just don't exist.
To be able to use Vim mode with those layouts & languages, you can turn on the "fixed keyboard layout" feature in the
plugin settings.

When turned on for the first time, or when you click "capture current layout", your current keyboard layout is saved,
and that will be the layout that is used when you are in Vim normal or visual mode.
When you enter insert mode, you will type in your actual current system layout/language.

**This feature is experimental and may have unintended side-effects relating to Obsidian or editor shortcuts.**

## Changelog

### 0.4.1
- Small fix in `surround`.

### 0.4.0
- `surround` and `pasteinto` commands (thanks @Andr3wD!)
- Vim chord display (thanks @Andr3wD!)
- Vim mode display (thanks @Andr3wD!)
- Fixed [fold and unfold bug](https://github.com/esm7/obsidian-vimrc-support/issues/35).
- The plugin now supports maintaining a fixed keyboard layout when in normal mode, if configured to do so.

### 0.3.1

- Fixed some commands not working via `obcommand` (https://github.com/esm7/obsidian-vimrc-support/issues/32)

### 0.3.0

- Added a settings file for the Vimrc file name (thank you @SalmanAlSaigal!)
- Added the `exmap` Ex command.
- Added the `obcommand` Ex command.

### 0.2.4

Fixed a race condition with yank & paste: https://github.com/esm7/obsidian-vimrc-support/issues/11

### 0.2.3

Added the `noremap` command, thanks @nadavspi!

### 0.2.2

Added the `iunmap` command, thanks @hnsol!

### 0.2.1

- Fixed [this issue](https://github.com/esm7/obsidian-vimrc-support/issues/7): setting `clipboard=unnamed` also works for pasting now (it monitors the system clipboard and updates the yank buffer if a change is detected).
- Support for the `tabstop` Vim option as asked [here](https://github.com/esm7/obsidian-vimrc-support/issues/3).

### 0.2.0

Added support for yanking to system clipboard (see above), comments and blank lines.

### 0.1.1

Fixed [an issue](https://github.com/esm7/obsidian-vimrc-support/issues/2) caused by the plugin injecting the Vimrc on every file load.
The plugin now injects the Vimrc just once for the CodeMirror class (for the class -- not object instance, because that's where CodeMirror keeps the Vim settings.)

This seems to work well, but in theory there could be Vimrc settings that are CodeMirror-object bound and not class-bound, and in that case we'll be in trouble (these settings will be lost when Obsidian replaces CodeMirror objects).
