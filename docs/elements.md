# Elements

Every element is added to a section, for example `Section:Toggle({...})`.

These options work on every element:

| Option | What it does |
|---|---|
| `Name` | the label |
| `Flag` | the name of the stored value |
| `Description` | text shown when you hover |
| `Icon` | a small icon before the label |
| `Callback` | your function, runs when the value changes |
| `Risky` | red label |
| `Locked` | disables it; the text you give becomes the hover text |
| `Visible` | `false` hides it |
| `ShowWhen` | only visible while a condition is true |
| `EnableWhen` | only usable while a condition is true |
| `Save` | `false` keeps it out of configs |

## Toggle

```lua
local esp = Section:Toggle({Name = "Enabled", Default = false, Keybind = "E", Callback = function(on) end})
```

- `Keybind` binds a key right away. Players can change it with right click.
- `Color = Color3.fromRGB(255, 0, 0)` adds a color square next to the switch.
- `Menu` opens a small panel of extra options from the row:

```lua
Section:Toggle({Name = "Box", Menu = function(menu)
	local card = menu.Card()
	card:Slider({Name = "Thickness", Min = 1, Max = 4, Default = 1})
	card:Dropdown({Name = "Style", Values = {"Full", "Corner"}})
end})
```

## Slider

```lua
Section:Slider({Name = "FOV", Min = 30, Max = 120, Default = 70, Step = 1, Suffix = "°", Callback = function(v) end})
```

`Live = false` runs the callback only when the mouse is released.

Change the range at any time:

```lua
local fov = Section:Slider({Name = "FOV", Min = 30, Max = 120, Default = 70})
fov:SetMax(1000)
fov:SetMin(1)
fov:SetStep(5)
fov:SetSuffix(" studs")
```

## Dropdown

```lua
Section:Dropdown({Name = "Part", Values = {"Head", "Torso", "Legs"}, Default = "Head"})
Section:Dropdown({Name = "Parts", Values = {"Head", "Torso", "Legs"}, Multi = true, Default = {"Head"}})
Section:Dropdown({Name = "Player", Special = "Players"})
Section:Dropdown({Name = "Team", Special = "Teams"})
Section:Dropdown({Name = "Material", Values = Enum.Material})
```

`Special = "Players"` lists the players in the server and updates when someone joins or leaves.

## Segmented

```lua
Section:Segmented({Name = "Mode", Values = {"Legit", "Rage"}, Default = "Legit"})
```

## ColorPicker

```lua
Section:ColorPicker({Name = "Color", Default = Color3.fromRGB(255, 80, 80), Alpha = 1, Callback = function(color, alpha) end})
```

## Input

```lua
Section:Input({Name = "Name", Placeholder = "Type here", Callback = function(text) end})
Section:Input({Name = "Amount", Numeric = true, Min = 1, Max = 100, Callback = function(number) end})
```

## Keybind

```lua
Section:Keybind({Name = "Teleport", Default = "T", Callback = function() end})
Section:Keybind({Name = "Sprint", Default = "LeftShift", Mode = "Hold", Callback = function(held) end})
```

`Mode` is `"Press"`, `"Toggle"` or `"Hold"`.

## Button and Buttons

```lua
Section:Button({Name = "Rejoin", Icon = "refresh-cw", Callback = function() end})
Section:Button({Name = "Delete", Variant = "Danger", Confirm = true, Callback = function() end})
Section:Buttons({
	{Name = "Save", Callback = function() end},
	{Name = "Load", Callback = function() end},
})
```

`Confirm = true` asks for a second click.

## Text

```lua
Section:Label("Plain text")
Section:Label({Text = "Something went wrong", Style = "Danger"})
Section:Paragraph({Title = "About", Body = "Longer text that wraps."})
local status = Section:Info({Name = "Status", Value = "Idle"})
status:Set("Running")
```

Label styles: `Muted`, `Info`, `Success`, `Warning` and `Danger`.

## Progress, Image and Console

```lua
local bar = Section:Progress({Name = "Loading", Value = 0})
bar:Set(0.5)

Section:Image({Source = "rbxassetid://123456", Height = 120})

local log = Section:Console({Height = 160})
log:Log("Started")
log:Warn("Careful")
log:Error("Failed")
```

## Spacing

```lua
Section:Divider("More")
Section:Spacer(12)
```

## Pages inside a section

```lua
local Modes = Tab:Section({Name = "Modes", Pages = {"Legit", "Rage"}})
```

Add elements to a page with `Page`:

```lua
local Weapons = Tab:Section("Weapons")
local rifle = Weapons:Page("Rifle")
local pistol = Weapons:Page("Pistol")
rifle:Toggle({Name = "Enabled"})
pistol:Slider({Name = "FOV", Min = 10, Max = 120, Default = 60})
```

## Conditions

`ShowWhen` and `EnableWhen` take:

- another element, for example `ShowWhen = speed`
- a flag and a value, for example `ShowWhen = {mode = "Rage"}`
- a function, for example `ShowWhen = function(flags) return flags.speed and flags.walk_speed > 50 end`

## Element methods

| Method | What it does |
|---|---|
| `:Get()` / `:Set(value)` | read or change the value |
| `:OnChanged(fn)` | run a function when the value changes |
| `:SetCallback(fn)` | replace the callback |
| `:SetName(text)` | change the label |
| `:SetVisible(bool)` | show or hide |
| `:Lock(reason)` / `:Unlock()` | disable or enable |
| `:MoveUp()` / `:MoveDown()` | change the order |
| `:Reset()` | back to the default value |
| `:Destroy()` | remove it |

Dropdowns also have `:SetValues(list)`, `:AddValues(list)` and `:RemoveValues(list)`.
