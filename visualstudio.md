![Ironhack Logo](https://i.imgur.com/uYvaMH6.png)

## Visual Studio 

### Most important shortcuts

Shortcut       | Explanation
---------------|---------------------------------------------------
`Cmd+X`        | Cut (if nothing selected, the all line is cut)
`Cmd+C`        | Copy (if nothing selected, the all line is copied)
`Cmd+V`        | Paste
`Cmd+F`        | Search on the current file
`Cmd+Shift+F`  | Search globally
`Cmd+P`        | Open the "Magic Box" to navigate throw files
`Cmd+Shift+P`  | Open the "Magic Box" to navigate throw VS commands
`Cmd+D`        | Add selection to next find match
`Alt+ArrowKey` | Move line up or down


### Plugins

#### For all modules
- **Live Server** (used by Maxence): Launch a development local Server with live reload feature for static & dynamic pages
- **Auto Rename Tag** (used by Maxence): Automatically rename paired HTML/XML tag, same as Visual Studio IDE does.
- **Markdown Preview Github Styling** (used by Maxence): Automatically rename paired HTML/XML tag, same as Visual Studio IDE does.


### VS Code Settings

To access your Visual Studio settings, `Cmd+Shit+P` > "*Open User Settings*" and then choose "..." > "*Open settings.json*" (or `Cmd+Shit+P` > "*Open Settings (JSON)*").

To create workspace settings, you can create a file `.vscode/settings.json` at the root of your project. 

```json
{
    "editor.tabSize": 2,
    "editor.minimap.enabled": false,
    "editor.formatOnSave": true,
    "editor.wordWrap": "on"
}
```