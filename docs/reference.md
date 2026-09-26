# Reference

## Arvn

| Method | What it does |
|---|---|
| `Arvn:CreateWindow(options)` | creates the window |
| `Arvn:Notify({Title, Content, Kind, Icon, Duration, Persist, Buttons})` | a notification; returns `SetTitle`, `SetBody`, `SetProgress`, `Dismiss` |
| `Arvn:Dialog({Title, Content, Icon, Buttons})` | a popup with buttons |
| `Arvn:Prompt({Title, Placeholder, Default, Callback})` | a popup with a text box |
| `Arvn:Widget({Name, Icon, Rows})` | a small panel on screen; `SetRow(key, value)`, `RemoveRow`, `Clear` |
| `Arvn:GetElement(flag)` | any element by flag, built-in ones included |
| `Arvn:OnFlag(flag, fn)` | run a function when a flag changes |
| `Arvn:Patch(instance, property, value)` | change a property and remember the original |
| `Arvn:Restore(instance, property)` | put the original back |
| `Arvn:Connect(signal, fn)` | a connection that stops on eject |
| `Arvn:Loop(fn, seconds)` | a loop that stops on eject; returns a stop function |
| `Arvn:Track(instance)` | destroyed on eject |
| `Arvn:OnEject(fn)` | runs on eject |
| `Arvn:OnReset(fn)` | runs when a player uses Reset Everything |
| `Arvn:SetWatermark({Text, Visible})` | watermark text and visibility |
| `Arvn:AddWatermarkPart(key, {Icon, Get})` | adds a live value to the watermark |
| `Arvn:AddFont(name, family)` | adds a menu font |
| `Arvn:SetNotifySide(side)` | `"Top Right"`, `"Top Left"`, `"Bottom Right"` or `"Bottom Left"` |
| `Arvn:Toggle(open)` | opens or closes the menu |
| `Arvn:Icons()` | every icon name |

| Field | What it is |
|---|---|
| `Arvn.Flags` | every value; setting one updates the menu |
| `Arvn.Theme` | `Register`, `Set`, `Get`, `List`, `SetColor`, `ResetColor`, `Bind`, `Export`, `Import`, `OnChanged` |
| `Arvn.Config` | `Save`, `Load`, `Delete`, `List`, `SetAutoload`, `Export`, `Import`, `Set`, `Get`, `ResetAll` |
| `Arvn.Errors` | errors from your callbacks; they are never printed |

## CreateWindow options

| Option | Default |
|---|---|
| `Title`, `Subtitle`, `Author`, `Version`, `Credits`, `Logo` | `"arvn"`, none, none, none, none, none |
| `Folder`, `SubFolder` | `"arvn"`, none |
| `MenuKey` | `"RightShift"` |
| `Theme`, `Accent`, `Colors` | `"Dark"` |
| `Width`, `Height`, `SidebarWidth`, `Resizable` | `880`, `640`, `188`, `true` |
| `Font`, `Scale`, `ToggleStyle` | `"BuilderSans"`, `100`, `"Switch"` |
| `Blur`, `Particles`, `Background` | `true`, `"Snow"`, none |
| `Watermark`, `WatermarkText`, `Keybinds`, `Keystrokes` | `true`, the title, `true`, `false` |
| `Search`, `OpenOnLoad`, `LoadNotification` | `true`, `true`, `true` |
| `NotifySide`, `Notifications`, `Sounds` | `"Top Right"`, `true`, `true` |
| `UIButton` | `true`; `false` hides it, `{Icon, Text}` changes it |
| `Dashboard`, `Server`, `Tools` | off |
| `KeySystem` | none; `{Title, Note, Keys, Check, Link, SaveKey}` |
| `Groups`, `Pages` | built-in names |

## Window

| Method | What it does |
|---|---|
| `Group(name)` | a sidebar heading |
| `Tab({Name, Icon, Description, Order, Locked, ShowWhen})` | a tab without a heading |
| `GetGroup(name)`, `GetTab(name)` | find a group or tab, built-in ones included |
| `SelectTab(tab)` | switch to a tab |
| `SetTitle`, `SetSubtitle`, `SetAuthor`, `SetLogo`, `SetSize(w, h)`, `SetBackground({...})` | change the window |
| `SetTheme`, `SetAccent`, `SetFont`, `SetScale`, `SetMenuKey` | change the look and key |
| `Toggle(open)`, `IsOpen()`, `Center()`, `OpenSearch()` | control the menu |
| `Minimize(bool)`, `IsMinimized()` | shrink the window to its title bar or bring it back |
| `OnOpen(fn)`, `OnClose(fn)` | run a function when the menu opens or closes |
| `LockAll(reason)`, `UnlockAll()` | disable every element, for example until a key is checked |
| `SaveConfig(name)`, `LoadConfig(name)` | configs |
| `Eject()` | turns everything off and removes the menu |

## Group, Tab, Section

| Handle | Methods |
|---|---|
| Group | `Tab`, `GetTab`, `SetName`, `SetVisible`, `SetOrder`, `Destroy` |
| Tab | `Section`, `SubTab`, `GetSection`, `GetSubTab`, `CustomPage`, `Select`, `SetName`, `SetIcon`, `SetDescription`, `SetVisible`, `SetOrder`, `Lock`, `Unlock`, `Destroy` |
| Section | every element, `Page`, `SetName`, `SetVisible`, `SetOrder`, `SetSide`, `Destroy` |

## Eject

Eject can be done from Settings, from the profile menu, or with `Window:Eject()`. It:

1. turns every toggle off, which runs their callbacks
2. puts back everything changed with `Patch`
3. stops every `Connect` and `Loop`
4. removes the menu
