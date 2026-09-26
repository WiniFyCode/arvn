# Customization

## Rename, hide and reorder

Groups, tabs, sections and elements can be changed at any time, including the built-in ones.

```lua
Window:GetGroup("Main"):SetName("Home")
Window:GetGroup("Settings"):SetName("Config")
Window:GetTab("Appearance"):SetName("Look")
Window:GetTab("Sounds"):SetVisible(false)

Player:SetName("Character"):SetIcon("person-standing")
Movement:SetName("Motion")
speed:SetName("Sprint")
```

| Method | Works on |
|---|---|
| `SetName`, `SetVisible`, `Destroy` | groups, tabs, sections, elements |
| `SetIcon`, `SetDescription`, `Lock`, `Unlock` | tabs |
| `SetOrder` | groups, tabs, sections |
| `SetSide("Left" or "Right")` | sections |
| `MoveUp`, `MoveDown`, `MoveTo` | elements |

Icons can be a name, an image link or an asset id. See [Icons](icons.md).

Built-in pages can also be renamed when the window is created:

```lua
Arvn:CreateWindow({
	Title = "My Script",
	Groups = {Main = "Home", Settings = "Config"},
	Pages = {Appearance = "Look", Profile = false},
})
```

## Themes

Built in: Dark, Gray, Blue, Green, Purple, Orange, Pink and Light.

```lua
Arvn:CreateWindow({Title = "My Script", Theme = "Blue"})
Arvn.Theme:Set("Green")
```

Make your own:

```lua
Arvn.Theme:Register("Ocean", {
	Background = Color3.fromRGB(10, 16, 24),
	Card = Color3.fromRGB(20, 30, 44),
	Text = Color3.fromRGB(235, 242, 250),
	Accent = Color3.fromRGB(80, 170, 255),
})
Arvn.Theme:Set("Ocean")
```

Colors you leave out are worked out from the others.

Players can also make their own theme in Settings > Appearance > Colors. Changing any color there switches the menu to the Custom theme.

Change one color on the current theme:

```lua
Arvn.Theme:SetColor("Accent", Color3.fromRGB(255, 120, 60))
Arvn.Theme:ResetColor("Accent")
```

Color names: `Background`, `Panel`, `Card`, `Field`, `Hover`, `Popup`, `Text`, `Label`, `Subtext`, `Dim` and `Accent`.

Share a theme as text:

```lua
local code = Arvn.Theme:Export()
Arvn.Theme:Import(code)
```

## Window

```lua
Arvn:CreateWindow({
	Title = "My Script",
	Subtitle = "v1",
	Logo = "rbxassetid://123456",
	Width = 900,
	Height = 640,
	Font = "GothamSSm",
	ToggleStyle = "Checkbox",
	Blur = false,
	Particles = "Off",
	Background = {Image = "https://files.catbox.moe/example.png", Darken = 0.4},
	NotifySide = "Bottom Right",
	MenuKey = "Insert",
})
```

- `ToggleStyle` is `"Switch"`, `"Square"` or `"Checkbox"`.
- `Particles` is `"Snow"`, `"Sparkles"`, `"Dust"` or `"Off"`.
- Players can also change most of these in Settings. Their choice is saved.

## Your own elements

`Custom` gives you an empty space inside a card.

```lua
Section:Custom({Name = "Health", Height = 30, Build = function(frame, ui)
	local bar = ui.Frame({Size = UDim2.fromScale(0.7, 1), BackgroundColor3 = ui.Accent(), Parent = frame})
	ui.Corner(bar, 6)
	ui.OnAccent(function(color) bar.BackgroundColor3 = color end)
end})
```

`ui` has the current colors (`ui.Theme`), `ui.Accent()`, and helpers: `Frame`, `Text`, `Button`, `Icon`, `Corner`, `Stroke`, `Tween` and `Connect`.

`Build` runs again when the menu redraws, for example after a theme change.

Turn a builder into a new element type:

```lua
Arvn:RegisterElement("Meter", {Height = 20, Default = 0, Build = function(frame, ui, options)
	local fill = ui.Frame({Size = UDim2.fromScale(ui.Get(), 1), BackgroundColor3 = options.Color or ui.Accent(), Parent = frame})
	ui.OnChanged(function(value) ui.Tween(fill, 0.3, {Size = UDim2.fromScale(value, 1)}) end)
end})

local load = Section:Meter({Name = "Load", Color = Color3.fromRGB(80, 220, 140)})
load:Set(0.8)
```

A whole page of your own:

```lua
Main:Tab({Name = "Canvas", Icon = "image"}):CustomPage(function(frame, ui)
	ui.Text({Text = "Anything goes here", Size = UDim2.new(1, 0, 0, 30), Parent = frame})
end)
```

## Keep your frames in theme colors

```lua
Arvn.Theme:Bind(myFrame, {BackgroundColor3 = "Card", BorderColor3 = "Accent"})
```

## Watermark

```lua
Arvn:SetWatermark({Text = "My Script"})
Arvn:AddWatermarkPart("kills", {Icon = "crosshair", Get = function() return "3 kills" end})
```
