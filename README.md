# scoot ui library

```lua
local UI = loadstring(game:HttpGet('https://raw.githubusercontent.com/Goatofhells/Scoot-uo/refs/heads/main/scootuilib.lua'))()
```

---

## Window

```lua
local Window = UI:Window({
    Logo     = "assetId",
    FadeTime = 0.3,
})
```

---

## Watermark & Keybind List

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

---

## Page

```lua
local Page = Window:Page({ Name = "Combat", Columns = 2 })
local Page = Window:Page({ Name = "Combat", SubPages = true })
```

---

## SubPage

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
    FadeTime = 0.3,
})

local Watermark   = UI:Watermark("my script")
local KeybindList = UI:KeybindList()
local Settings    = UI:CreateSettingsPage(Window, Watermark, KeybindList)

local CombatPage  = Window:Page({ Name = "Combat", SubPages = true })
local PlayerPage  = Window:Page({ Name = "Player", Columns = 2 })

local AimbotSub   = CombatPage:SubPage({ Name = "Aimbot", Columns = 2 })
local WeaponSub   = CombatPage:SubPage({ Name = "Weapon", Columns = 2 })

local AimbotSection = AimbotSub:Section({ Name = "Silent Aim", Side = 1 })

local SilentAim = AimbotSection:Toggle({
    Name     = "Enabled",
    Flag     = "SilentAimEnabled",
    Default  = false,
    Callback = function(Value)
        print("Silent Aim:", Value)
    end,
})

SilentAim:Keybind({
    Flag     = "SilentAimKeybind",
    Default  = Enum.KeyCode.E,
    Mode     = "Toggle",
    Callback = function(Value)
        print("Keybind toggled:", Value)
    end,
})

AimbotSection:Slider({
    Name     = "FOV Radius",
    Flag     = "FOVRadius",
    Min      = 1,
    Max      = 500,
    Default  = 75,
    Decimals = 1,
    Suffix   = "px",
    Callback = function(Value)
        print("FOV:", Value)
    end,
})

AimbotSection:Dropdown({
    Name     = "Bone",
    Flag     = "AimbotBone",
    Default  = "Head",
    Multi    = false,
    Items    = {"Head", "Neck", "Torso", "LeftArm", "RightArm"},
    Callback = function(Value)
        print("Bone:", Value)
    end,
})

local PlayerSection = PlayerPage:Section({ Name = "Movement", Side = 1 })

PlayerSection:Toggle({
    Name     = "Speed Hack",
    Flag     = "SpeedHack",
    Default  = false,
    Callback = function(Value)
        print("Speed Hack:", Value)
    end,
})

PlayerSection:Slider({
    Name     = "Walk Speed",
    Flag     = "WalkSpeed",
    Min      = 16,
    Max      = 500,
    Default  = 16,
    Decimals = 1,
    Suffix   = "studs/s",
    Callback = function(Value)
        game.Players.LocalPlayer.Character.Humanoid.WalkSpeed = Value
    end,
})

local MiscSection = PlayerPage:Section({ Name = "Misc", Side = 2 })

MiscSection:Button():Add("Rejoin", function()
    local TS = game:GetService("TeleportService")
    local LP = game.Players.LocalPlayer
    TS:TeleportToPlaceInstance(game.PlaceId, game.JobId, LP)
end)

UI:Notification("Loaded", "Script loaded successfully", 5)
```
