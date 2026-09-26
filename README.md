<p align="center">
  <img src="assets/hero.png" alt="arvn lib" width="100%">
</p>

<h1 align="center">arvn lib</h1>

<p align="center">UI library for Roblox.</p>

<p align="center">
  <a href="docs/getting-started.md">Getting started</a>
  &nbsp;·&nbsp;
  <a href="docs/elements.md">Elements</a>
  &nbsp;·&nbsp;
  <a href="docs/customization.md">Customization</a>
  &nbsp;·&nbsp;
  <a href="docs/icons.md">Icons</a>
  &nbsp;·&nbsp;
  <a href="docs/reference.md">Reference</a>
  &nbsp;·&nbsp;
  <a href="example.lua">Example</a>
</p>

<br>

```lua
local Arvn = loadstring(game:HttpGet("https://raw.githubusercontent.com/koteqjjjj/arvn/main/arvn.lua"))()
```

<br>

<table>
  <tr>
    <td><img src="assets/player.png" alt="Sections and option menus"></td>
    <td><img src="assets/theme.png" alt="Themes and color picker"></td>
  </tr>
  <tr>
    <td><img src="assets/keybind.png" alt="Keybinds"></td>
    <td><img src="assets/light.png" alt="Light theme"></td>
  </tr>
  <tr>
    <td><img src="assets/search.png" alt="Search"></td>
    <td><img src="assets/home.png" alt="Dashboard"></td>
  </tr>
</table>

## Example

```lua
local Arvn = loadstring(game:HttpGet("https://raw.githubusercontent.com/koteqjjjj/arvn/main/arvn.lua"))()

local Window = Arvn:CreateWindow({Title = "My Script", Author = "you", Folder = "MyScript"})

local Main = Window:Group("Main")
local Player = Main:Tab({Name = "Player", Icon = "user"})
local Movement = Player:Section("Movement")

local speed = Movement:Toggle({Name = "Speed", Keybind = "V", Callback = function(on) end})
Movement:Slider({Name = "Walk Speed", Min = 16, Max = 100, Default = 32, ShowWhen = speed})
Movement:Button({Name = "Reset", Callback = function() end})
```

The full example is in [example.lua](example.lua).

## Credits

arvn lib by [koteqjjjj](https://github.com/koteqjjjj). Icons by [Lucide](https://lucide.dev).
