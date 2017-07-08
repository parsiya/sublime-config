# Setting up Sublime Text
I have moved from Atom to Sublime. Atom is a nice editor with a lot of features but it has a lot of performance issues for what I want to do.

Below is my setup for reference. When I want to do it again in a year (or a new machine) I can just use everything here or just use the config files.

<!-- MarkdownTOC -->

- [Install Package Control](#install-package-control)
- [Install Packages](#install-packages)
- [Markdown Packages](#markdown-packages)
- [How to Use the Config Files](#how-to-use-the-config-files)
- [Package Settings and Locations](#package-settings-and-locations)
- [Markdown Highlighting and Spell Check](#markdown-highlighting-and-spell-check)
- [Setting up Markdown Live Preview](#setting-up-markdown-live-preview)
	- [Enable LiveReload via Settings](#enable-livereload-via-settings)
	- [Enable LiveReload Manually \(need to do after every Sublime launch\)](#enable-livereload-manually-need-to-do-after-every-sublime-launch)
	- [Configure Markdown Preview](#configure-markdown-preview)
	- [Preview Files](#preview-files)
	- [Preview Keybind](#preview-keybind)
- [Markdown Table of Content](#markdown-table-of-content)
	- [TOC Keybind](#toc-keybind)

<!-- /MarkdownTOC -->


<a name="install-package-control"></a>
## Install Package Control
Install package control using: https://packagecontrol.io/installation.

<a name="install-packages"></a>
##  Install Packages
Now you can install packages.

1. Press `Ctrl+Shift+P` to open the command palette.
2. Type `Install` and then select `Package Control: Install Package`.
3. Type the name of the package you are looking for to search for it.
4. Select the package and press Enter.

<a name="markdown-packages"></a>
##  Markdown Packages

1. Markdown Extended: Syntax highlighting.
2. Markdown Preview.
3. Markdown Editing: Shortcut keys (e.g. ctrl+1 means heading 1).
4. Monokai Extended: Need this for the highlighting.
5. LiveReload: For live markdown preview.
6. MarkdownTOC: Automatically generate clickable table of contents to markdown documents.

<a name="how-to-use-the-config-files"></a>
## How to Use the Config Files
After installing packages, just copy the config files to the user package settings directory. On Windows it will be `"%Appdata%\Sublime Text 3\Packages\User\"` (don't forget the double quotes if you want to just paste it into the run prompt).

<a name="package-settings-and-locations"></a>
##  Package Settings and Locations
Generally sublime and each package have two types of settings, default and user. User settings are used to override default ones. Both are in JSON.

Settings can be opened via `Preferences > Package Settings > Settings Default/User`. I usually copy from default file to user, remove the unneeded settings and override the rest.

Package settings on Windows are at `%Appdata%\Sublime Text 3\Packages\User\package-name.sublime-settings`.

Main settings can be overridden in `Preferences.sublime-settings` or accessed via `Preferences > Settings`. This will open two files in one window. Left are the defaults settings and right is the user settings file. Copy from left pane to the right one and override.

<a name="markdown-highlighting-and-spell-check"></a>
##  Markdown Highlighting and Spell Check
`Markdown Editing` has its own color scheme. I don't like it. Instead I use `Monokai Extended`. It can be selected from `Preferences > Color Scheme > Monokai Extended > Monokai Extended`.

In order for it to kick in, the document type need to be set to `Markdown Extended`. This can be set by clicking on document type (bottom right).

Next you want to set all markdown files to be opened as `Markdown Extended` for syntax highlighting (including code blocks). This can be done by:

- `View (menu) > Syntax > Open all with current extension as > Markdown Extended`.

This method only sets it for the current extension (e.g. md).

Go to `Preferences > Settings - Syntax Specific` or edit package settings `Markdown Extended.sublime-settings` and add the following:

``` json
{
	"extensions":
	[
		"md",
		"markdown",
		"moreextensions"
	],
	"spell_check": true	// enable spell check
}
```

Note that `Markdown Editing` has added itself for `.mdown` files. You can just delete the file `Markdown.sublime-settings` and add the extensions in the previous file.

<a name="setting-up-markdown-live-preview"></a>
##  Setting up Markdown Live Preview

<a name="enable-livereload-via-settings"></a>
###  Enable LiveReload via Settings
Add the following to user settings for the LiveReload package `LiveReload.sublime-settings`:

``` json
{
     "enabled_plugins": [
     	"SimpleReloadPlugin",
     	"SimpleRefreshDelay"	// use SimpleRefresh for reload without delay
     ]
}
```
This way it does not need to be re-enabled after every start.

<a name="enable-livereload-manually-need-to-do-after-every-sublime-launch"></a>
###  Enable LiveReload Manually (need to do after every Sublime launch)
1. Open command palette and type `livereload`.
2. Select `LiveReload: Enable/disable plug-ins`.
3. Select `Enable - Simple Reload with delay(400ms)`.
4. You should see a console message saying it was enabled. Note that the menu will say `Enable` whether it's enabled or not, if it's already enabled choosing the menu will disable it so make sure to look at the console messages.

<a name="configure-markdown-preview"></a>
###  Configure Markdown Preview
Supposedly these two plugins work out of the box. It was not in my case. I had to add autoreload in markdown preview. I removed the `github` parser because it sends the markdown file to Github to be processed.

Add the following to `MarkdownPreview.sublime-settings`:

``` json
{
	"enable_autoreload": true,
	"enabled_parsers": ["markdown"],
	"enable_highlight": true
}
```

<a name="preview-files"></a>
###  Preview Files
1. Open command palette and select `Markdown Preview: Preview in Browser`.
2. A new browser window will open to display the rendered document.
2. Browser should update after every save.

<a name="preview-keybind"></a>
### Preview Keybind
Add the following to `Default (Windows).sublime-keymap` or open it via `Preferences > Key Bindings`.

``` json
[
	{
	"keys": [
		"alt+p"
	],
	"command": "markdown_preview",
	"args": {
		"target": "browser",
		"parser": "markdown"
	}
	}
]
```

<a name="markdown-table-of-content"></a>
##  Markdown Table of Content
1. Install package `Markdown TOC`.
2. Add the following user settings to `MarkdownTOC.sublime-settings`:

``` json
{
	"default_autoanchor": true,  // adds anchor to headings in not present
  	"default_autolink": true,	 // make the ToC linkable
  	"default_bracket": "round",  // use parentheses for link (e.g. [linktext](linkreference)) otherwise both will be brackets (square)
  	"default_depth": 0  // 0 = unlimited depth
}
```
3. In any markdown document, put the cursor where you want the T0C. Then `Tools > MarkdownTOC > Insert TOC`.
4. All settings can also be controlled in the T0C by adding them to the top comment. For example:

```
<!-- MarkdownTOC style="round" autolink="true" depth=0 -->

- [Heading 1]
- [Heading 2]

<!-- /MarkdownTOC -->
```

<a name="toc-keybind"></a>
### TOC Keybind
Add the following to the keymap `Default (Windows).sublime-keymap`:

``` json
{
	"keys": [
		"alt+t"
	],
	"command": "markdowntoc_insert"  // update is markdowntoc_update
}
```
