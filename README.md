# scoot ui library

![preview](https://raw.githubusercontent.com/Goatofhells/Scoot-uo/refs/heads/main/Screenshot_20260307-002712.Roblox.png)

```lua
local UI = loadstring(game:HttpGet('https://raw.githubusercontent.com/Goatofhells/Scoot-uo/refs/heads/main/scootuilib.lua'))()
```

---

## Window

`Name` and `Size` are optional. If `Name` is provided it appears above the logo in the sidebar.

```lua
local Window = UI:Window({
    Logo     = "assetId",
    Name     = "My Script",
    FadeTime = 0.3,
    Size     = UDim2.new(0, 751, 0, 539),
})
```

---

## Watermark & Keybind List *(optional)*

Both are optional. If you don't need them, skip them and pass `nil` to `CreateSettingsPage`.

```lua
local Watermark   = UI:Watermark("text")
local KeybindList = UI:KeybindList()

Watermark:SetVisibility(true)
KeybindList:SetVisibility(true)
```

---

## Settings Page

```lua
local Settings = UI:CreateSettingsPage(Window, Watermark, KeybindList)
```

Pass `nil` for Watermark and/or KeybindList if you didn't create them:

```lua
local Settings = UI:CreateSettingsPage(Window, nil, nil)
```

---

## Set Font *(optional)*

Call after `UI:Window()`. Pass any Roblox font asset ID.

```lua
UI:SetFont(12187375716)
```

---

## Mobile Toggle *(optional)*

A separate draggable image button that floats at the top of the screen to toggle the whole GUI. If no icon is provided nothing is created and no error is thrown.

```lua
UI:MobileToggle(Window, 116262397243671)
```

Pass any Roblox asset ID as the icon number — no `rbxassetid://` prefix needed. Omit the call entirely if you don't need it.

---

## Page

```lua
local Page = Window:Page({ Name = "Combat", Columns = 2 })
local Page = Window:Page({ Name = "Combat", SubPages = true })
```

---

## SubPage

Requires the page to have `SubPages = true`.

```lua
local Sub = Page:SubPage({ Name = "Silent Aim", Columns = 2 })
```

---

## Section

```lua
local Section = Page:Section({ Name = "Title", Side = 1 })
```

`Side = 1` left · `Side = 2` right

---

## Toggle

```lua
local Toggle = Section:Toggle({
    Name     = "Enabled",
    Flag     = "MyFlag",
    Default  = false,
    Callback = function(Value) end,
})

Toggle:Set(false)
Toggle:Get()
Toggle:SetVisibility(true)
```

---

## Slider

```lua
local Slider = Section:Slider({
    Name     = "Speed",
    Flag     = "MyFlag",
    Min      = 0,
    Max      = 100,
    Default  = 50,
    Decimals = 1,
    Suffix   = "px",
    Callback = function(Value) end,
})

Slider:Set(50)
Slider:Get()
Slider:SetVisibility(true)
```

---

## Dropdown

```lua
local Dropdown = Section:Dropdown({
    Name     = "Mode",
    Flag     = "MyFlag",
    Default  = "Option1",
    Multi    = false,
    Items    = {"Option1", "Option2", "Option3"},
    Callback = function(Value) end,
})

Dropdown:Set("Option1")
Dropdown:Get()
Dropdown:Add("Option4")
Dropdown:Remove("Option4")
Dropdown:Refresh({"Option1", "Option2"}, false)
Dropdown:SetVisibility(true)
```

---

## Searchbox

```lua
local Searchbox = Section:Searchbox({
    Name     = "Search",
    Flag     = "MyFlag",
    Default  = "Option1",
    Multi    = false,
    Items    = {"Option1", "Option2"},
    Callback = function(Value) end,
})

Searchbox:Set("Option1")
Searchbox:Get()
Searchbox:Add("Option3")
Searchbox:Remove("Option3")
Searchbox:Refresh({"Option1", "Option2"}, false)
Searchbox:SetVisibility(true)
```

---

## Textbox

```lua
local Textbox = Section:Textbox({
    Name        = "Input",
    Flag        = "MyFlag",
    Default     = "",
    Placeholder = "Type here...",
    Numeric     = false,
    Finished    = false,
    Callback    = function(Value) end,
})

Textbox:Set("hello")
Textbox:Get()
Textbox:SetVisibility(true)
```

---

## Button

```lua
local Button = Section:Button()
Button:Add("Apply", function() end)
Button:Add("Reset", function() end)
```

---

## Image Button

Same as Button but each entry has an icon. Pass a Roblox asset ID as the icon number.

```lua
local IB = Section:ImageButton()
IB:Add("Rejoin",   6031302502, function() end)
IB:Add("Teleport", 6031068421, function() end)
```

`IB:Add(label, iconId, callback)` → `NewButton`
`NewButton:Press()`
`NewButton:SetVisibility(bool)`

---

## Divider

A horizontal line to visually separate elements. Optionally shows a label in the center.

```lua
Section:Divider()
Section:Divider("Combat")
```

`Divider:SetVisibility(bool)`

---

## Progress

A read-only progress bar. Update it manually via `:Set()`.

```lua
local Bar = Section:Progress({
    Name    = "Health",
    Flag    = "HealthBar",
    Min     = 0,
    Max     = 100,
    Default = 100,
    Suffix  = "%",
})

Bar:Set(75)
Bar:Get()
Bar:SetVisibility(true)
```

---

## Label

```lua
local Label = Section:Label("My Label")
Label:SetText("New Text")
Label:SetVisibility(true)
```

---

## Colorpicker

Chains on `Label` or `Toggle`.

```lua
local CP = Label:Colorpicker({
    Name     = "Color",
    Flag     = "MyFlag",
    Default  = Color3.fromRGB(169, 242, 112),
    Alpha    = 0,
    Callback = function(Value) end,
})

CP:Set(Color3.fromRGB(169, 242, 112), 0)
CP:Get()
CP:SetVisibility(true)
```

```lua
Toggle:Colorpicker({
    Name     = "Color",
    Flag     = "MyFlag",
    Default  = Color3.fromRGB(169, 242, 112),
    Alpha    = 0,
    Callback = function(Value) end,
})
```

---

## Keybind

Chains on `Label` or `Toggle`. Modes: `Hold` · `Toggle` · `Always`

```lua
local KB = Label:Keybind({
    Flag     = "MyFlag",
    Default  = Enum.KeyCode.F,
    Mode     = "Hold",
    Callback = function(Value) end,
})

KB:Set(Enum.KeyCode.F)
KB:Get()
KB:SetMode("Toggle")
KB:Press()
```

```lua
Toggle:Keybind({
    Flag     = "MyFlag",
    Default  = Enum.KeyCode.E,
    Mode     = "Toggle",
    Callback = function(Value) end,
})
```

---

## Notification

```lua
UI:Notification("Title", "Description", 5)
```

---

## Theme

```lua
UI:ChangeTheme("Accent", Color3.fromRGB(169, 242, 112))
```

Keys: `Background` · `Border` · `Inline` · `Hovered Element` · `Page Background` · `Outline` · `Element` · `Gradient` · `Text` · `Text Stroke` · `Placeholder Text` · `Accent`

---

## Flags

```lua
UI.Flags["MyFlag"]
```

---

## Configs

```lua
UI:GetConfig()
UI:LoadConfig("name")
UI:SaveConfig("name")
UI:DeleteConfig("name")
```

---

## Unload

```lua
UI:Unload()
```

---

## Example Script

```lua
local UI = loadstring(game:HttpGet('https://raw.githubusercontent.com/Goatofhells/Scoot-uo/refs/heads/main/scootuilib.lua'))()

local Window = UI:Window({
    Logo     = "77218680285262",
    Name     = "My Script",
    FadeTime = 0.3,
})

UI:SetFont(12187375716)
UI:MobileToggle(Window, 116262397243671)

local Settings = UI:CreateSettingsPage(Window, nil, nil)

local CombatPage = Window:Page({ Name = "Combat", SubPages = true })
local Sub = CombatPage:SubPage({ Name = "Silent Aim", Columns = 2 })
local Section = Sub:Section({ Name = "Title", Side = 1 })

Section:Divider("Toggles")

local Toggle = Section:Toggle({
    Name     = "Enabled",
    Flag     = "MyFlag",
    Default  = false,
    Callback = function(Value)
        print(Value)
    end,
})

local Teleport = Section:Toggle({
    Name     = "Teleport",
    Flag     = "TeleportEnabled",
    Default  = false,
    Callback = function(Value)
        print(Value)
    end,
})

Section:Divider("Actions")

local IB = Section:ImageButton()
IB:Add("Rejoin", 6031302502, function() end)

Section:Divider("Stats")

local Bar = Section:Progress({
    Name    = "Health",
    Flag    = "HealthBar",
    Min     = 0,
    Max     = 100,
    Default = 100,
    Suffix  = "%",
})

Bar:Set(75)
```
