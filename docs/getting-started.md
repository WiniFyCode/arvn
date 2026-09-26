# Getting started

## Load

```lua
local Arvn = loadstring(game:HttpGet("https://raw.githubusercontent.com/koteqjjjj/arvn/main/arvn.lua"))()
```

## Create a window

```lua
local Window = Arvn:CreateWindow({
	Title = "My Script",
	Author = "your name",
	Version = "1.0",
	Folder = "MyScript",
})
```

- `Title` shows in the sidebar and the watermark.
- `Author` and `Version` show in Settings > General > About.
- `Folder` is the folder in `workspace` where the script's settings and configs are saved. Give every script its own folder.

The menu opens and closes with **Right Shift**. Change the default with `MenuKey = "Insert"`.

## Add pages

A window is split into groups, tabs and sections.

```
Window
  Group     a heading in the sidebar
    Tab     a page
      Section   a card on the page
```

```lua
local Main = Window:Group("Main")
local Player = Main:Tab({Name = "Player", Icon = "user"})
local Movement = Player:Section("Movement")
```

- Sections fill the left column first, then the right. To choose, use `Player:Section({Name = "Movement", Side = "Right"})`.
- Icons are names from [lucide.dev/icons](https://lucide.dev/icons).
- A tab can hold other tabs: `Player:SubTab({Name = "Camera", Icon = "camera"})`.

## Add elements

```lua
local speed = Movement:Toggle({
	Name = "Speed",
	Keybind = "V",
	Callback = function(on)
		print("Speed is", on)
	end,
})

Movement:Slider({
	Name = "Walk Speed",
	Flag = "walk_speed",
	Min = 16,
	Max = 100,
	Default = 32,
	Callback = function(value)
		print("Walk speed is", value)
	end,
})

Movement:Button({
	Name = "Reset",
	Callback = function()
		Arvn:Notify({Title = "Reset", Content = "Done."})
	end,
})
```

`Callback` runs your code every time the value changes. See [Elements](elements.md) for every element.

## Read values

Every element stores its value under a flag. Set the name with `Flag`, or one is made for you.

```lua
print(Arvn.Flags.walk_speed)
Arvn.Flags.walk_speed = 50
print(speed:Get())
speed:Set(true)
```

Setting a value updates the menu and runs the callback.

## Change the game safely

Use `Patch` to change a property. It remembers the original value and puts it back when you call `Restore` or when the menu is ejected.

```lua
local humanoid = game.Players.LocalPlayer.Character.Humanoid
Arvn:Patch(humanoid, "WalkSpeed", 50)
Arvn:Restore(humanoid, "WalkSpeed")
```

Use `Arvn:Connect` and `Arvn:Loop` for events and loops so they stop on eject too.

```lua
Arvn:Connect(game:GetService("RunService").Heartbeat, function() end)
local stop = Arvn:Loop(function() end, 1)
```

## What is built in

Every window comes with:

- Settings pages: General, Appearance, Overlays, Profile, Sounds and Configs
- a watermark and a keybind list
- a UI button on screen that opens and closes the menu
- a minimize button next to the close button
- the executor name in the watermark and in About
- search, notifications, sounds and autosave

Turn any of them off:

```lua
Arvn:CreateWindow({
	Title = "My Script",
	Watermark = false,
	Keybinds = false,
	UIButton = false,
	Search = false,
	Sounds = false,
	Notifications = false,
	Pages = {Profile = false, Sounds = false},
})
```

Players can turn them back on in Settings. Their choice is saved.

Three optional pages can be turned on: `Dashboard = true`, `Server = true` and `Tools = true`.

## Key system

Ask for a key before the menu opens:

```lua
Arvn:CreateWindow({
	Title = "My Script",
	KeySystem = {
		Title = "My Script Key",
		Note = "Get a key from the link.",
		Keys = {"key-one", "key-two"},
		Link = "https://example.com/get-key",
	},
})
```

- `Get Key` copies `Link`.
- A correct key is saved, so the player only enters it once. Set `SaveKey = false` to ask every time.
- To check keys yourself, use `Check = function(key) return key == "abc" end` instead of `Keys`.

## Reset

Settings > Configs has two buttons:

- **Reset Settings** puts every option back to default and keeps configs.
- **Reset Everything** also deletes everything saved in the script's `Folder`: configs, autosave, window position and pictures.

You don't need to write any code for this. If your script saves its own files, clean them up with `OnReset`:

```lua
Arvn:OnReset(function()
	delfile("MyScript/stats.json")
end)
```

## Credits

Put your name in `Author`, and anyone else in `Credits`:

```lua
Arvn:CreateWindow({
	Title = "My Script",
	Author = "you",
	Credits = {{"UI Design", "friend"}, {"Testing", "someone"}},
})
```

They show in Settings > General > About, next to the arvn lib credit.

## Next

- [Elements](elements.md)
- [Customization](customization.md)
- [Reference](reference.md)
