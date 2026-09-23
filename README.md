markdown
# Library

A modern, fully customizable Roblox UI library — built for developers who want beautiful, feature-rich interfaces without writing UI code from scratch.

<p align="center">
  <b>Clean • Customizable • Mobile-Ready • Actively Maintained</b>
</p>

---

## Table of Contents

- [Features](#features)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Window Options](#window-options)
- [Tabs](#tabs)
- [Sections](#sections)
- [Components](#components)
- [Themes](#themes)
- [Fonts](#fonts)
- [Icons](#icons)
- [Key System](#key-system)
- [HWID & Security](#hwid--security)
- [Blocklist](#blocklist)
- [License System](#license-system)
- [Profiles](#profiles)
- [Macros](#macros)
- [Notifications](#notifications)
- [Widgets](#widgets)
- [Effects & Transitions](#effects--transitions)
- [Sounds](#sounds)
- [Utilities](#utilities)
- [Mobile Support](#mobile-support)
- [For Library Users](#for-library-users)
- [FAQ](#faq)
- [License](#license)

---

## Features

### Visual
- **6 Built-in Themes** — Dark, Neon, Cyberpunk, Pastel, Matrix, Blood
- **Animated Theme Mode** — Accent color cycles smoothly through the hue spectrum
- **Custom Theme Support** — Pass your own color palette
- **39 System Fonts** — Full control over typography
- **3 Window Modes** — Compact, Normal, Wide
- **Splash Screen** — Customizable loading screen with progress bar
- **Snap to Edge** — Auto-align windows to screen borders
- **UI Scaling** — Global and per-window scaling
- **Hover Animations** — Smooth tweened interactions
- **Accent Strip & Gradient Background**

### Systems
- **Key System** — Local or remote validation with optional webhook logging
- **HWID Detection** — Automatic hardware ID with SHA-256 hashing
- **Encryption Utilities** — SHA-256, XOR cipher, Base64 encode/decode
- **Blocklist** — Block by HWID, UserID, or Key (local + remote)
- **License Manager** — Tiered plans (free, basic, pro, premium, lifetime)
- **Profiles** — Save, load, delete, and switch configurations
- **Macros** — Record and replay action sequences
- **Import / Export** — Share configs via Base64 strings
- **Discord Webhook Logger** — Optional logging to any Discord channel

### UX
- **Notifications** — Full-size with images and 4 types (info, success, warning, error)
- **Toast** — Quick center-screen feedback
- **Snackbar** — Bottom-screen action bar with buttons
- **Confirm Dialog** — Yes/No confirmation modal
- **Prompt Dialog** — Text input modal
- **Global Search** — Search across all tabs and elements
- **Widgets** — FPS, Ping, Memory, Clock, or custom
- **Streamer Mode** — Larger UI, hidden sensitive info

### Components
Over 20 UI elements available out of the box — see [Components](#components).

### Compatibility
- **PC, Mobile, and Console** with automatic platform detection
- **Multi-Executor** — Synapse, Krnl, Fluxus, SirHurt, Sentinel, and more
- **Optional Obfuscation Hooks** — `syn.protect_gui` and `gethui` support

---

## Installation

### Via Loadstring

```lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/USER/REPO/main/library.lua"))()
```

> Replace the URL with the raw link to this repository's `library.lua` file.

### Recommended Repository Structure

```
your-repo/
├── library.lua          — Main library file
├── README.md
├── LICENSE
└── examples/
    ├── basic.lua
    ├── key_system.lua
    └── advanced.lua
```

---

## Quick Start

```lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/USER/REPO/main/library.lua"))()

local Window = Library:CreateWindow({
    Name = "My Hub",
    Subtitle = "v1.0",
    Theme = "Dark",
    Font = "Gotham",
    Splash = { Title = "My Hub", LogoText = "M" }
})

local Tab = Window:CreateTab("Main", "home")
local Section = Tab:CreateSection({ Name = "Actions", Collapsible = true })

Section:CreateButton({
    Name = "Click Me",
    Icon = "play",
    Callback = function()
        Library:Notify({ Title = "Success", Text = "It works!", Type = "success" })
    end
})

Section:CreateToggle({
    Name = "Enable Feature",
    Default = false,
    Callback = function(state) print(state) end
})

Section:CreateSlider({
    Name = "Volume",
    Min = 0, Max = 100, Default = 50,
    Callback = function(value) print(value) end
})
```

---

## Window Options

| Option | Type | Default | Description |
|---|---|---|---|
| `Name` | string | `"Library"` | Window title |
| `Subtitle` | string | `"v"..Version` | Subtitle line |
| `Icon` | string | `nil` | Logo icon (asset id or registered name) |
| `Theme` | string | `"Dark"` | Theme name |
| `CustomTheme` | table | `nil` | Custom color palette |
| `AnimatedTheme` | string | `nil` | Base theme for animated accent |
| `Font` | string | `"Gotham"` | Font family |
| `FontBold` | string | auto | Bold variant |
| `FontMedium` | string | auto | Medium variant |
| `Width` / `Height` | number | `620` / `420` | Normal mode size |
| `CompactWidth` / `CompactHeight` | number | `480` / `320` | Compact mode size |
| `WideWidth` / `WideHeight` | number | `840` / `480` | Wide mode size |
| `TabWidth` | number | `170` | Sidebar width |
| `ToggleKeys` | table | `{RightControl}` | Keys to toggle visibility |
| `SnapToEdge` | bool | `true` | Auto-align to screen edges |
| `AskPlatform` | bool | `true` | Ask PC/Mobile on first run |
| `Splash` | table | `nil` | Splash screen config |
| `Key` | table | `nil` | Key system config |
| `Blocklist` | table | `nil` | Blocklist config |
| `Sounds` | table | `nil` | Sound configuration |
| `OnClose` | function | `nil` | Callback when window closes |

---

## Tabs

```lua
local Tab = Window:CreateTab("Name", "icon")
```

### Tab Methods

```lua
Tab:SetName("New Name")
Tab:SetAccent(Color3.fromRGB(255, 0, 0))
Tab:SetTheme("Neon")
Tab:Destroy()
```

Tabs support **drag-to-reorder** — drag from the left edge of any tab button.

---

## Sections

```lua
local Section = Tab:CreateSection({
    Name = "Section Title",
    Collapsible = true,    -- default: true
    Collapsed = false      -- default: false
})
```

Sections group related components. Collapse them with a click on the header.

---

## Components

### Button

```lua
Section:CreateButton({
    Name = "Button",
    Icon = "play",
    Callback = function() end,
    Active = function() return someBool end   -- optional visual state
})
```

### Toggle

```lua
Section:CreateToggle({
    Name = "Toggle",
    Default = false,
    Callback = function(state) end
})
```

### Slider

```lua
Section:CreateSlider({
    Name = "Slider",
    Min = 0, Max = 100, Default = 50,
    Round = true,
    Suffix = "%",
    FillColor = Color3.fromRGB(255, 80, 200),
    BarColor = Color3.fromRGB(100, 40, 80),
    Callback = function(value) end
})
```

### Range Slider

```lua
Section:CreateRangeSlider({
    Name = "Range",
    Min = 0, Max = 100,
    DefaultMin = 20, DefaultMax = 80,
    Callback = function(min, max) end
})
```

### Input

```lua
Section:CreateInput({
    Name = "Input",
    Default = "",
    Placeholder = "Type here...",
    Callback = function(text, enterPressed) end
})
```

### Dropdown

```lua
Section:CreateDropdown({
    Name = "Dropdown",
    Options = {"Option 1", "Option 2", "Option 3"},
    Default = "Option 1",
    Callback = function(selected) end
})
```

### Multi Select

```lua
Section:CreateMultiSelect({
    Name = "Multi",
    Options = {"A", "B", "C"},
    Default = {"A"},
    Callback = function(selectedTable) end
})
```

### Color Picker

```lua
Section:CreateColorPicker({
    Name = "Color",
    Default = Color3.fromRGB(148, 132, 232),
    Callback = function(color) end
})
```

### Keybind / Bind

```lua
Section:CreateKeybind({
    Name = "Keybind",
    Default = Enum.KeyCode.F,
    Callback = function(keyCode) end
})
```

### Progress

```lua
local p = Section:CreateProgress({ Name = "Loading", Color = nil })
p:Set(0.75)   -- 75%
```

### Image

```lua
Section:CreateImage({
    Image = "rbxassetid://123456789",
    Height = 120
})
```

### Search (per tab)

```lua
Section:CreateSearch({
    Placeholder = "Search...",
    Callback = function(query) end
})
```

### Mini Tabs

```lua
Section:CreateMiniTabs({
    Tabs = {"One", "Two", "Three"},
    Callback = function(name, index) end
})
```

### Label / Paragraph / Divider

```lua
Section:CreateLabel({ Text = "Info text", Type = "info" })       -- info | success | warning | error
Section:CreateParagraph({ Title = "Title", Text = "Body" })
Section:CreateDivider()
```

---

## Themes

### Built-in Themes

`Dark` · `Neon` · `Cyberpunk` · `Pastel` · `Matrix` · `Blood`

```lua
Library:SetTheme("Neon")
```

### Animated Theme

```lua
Library:SetAnimatedTheme("Dark")   -- accent cycles through hue
```

### Custom Theme

```lua
Library:SetCustomTheme({
    Bg = Color3.fromRGB(20, 20, 20),
    Surface = Color3.fromRGB(30, 30, 30),
    Card = Color3.fromRGB(40, 40, 40),
    -- ... (see Palette structure in source)
})
```

---

## Fonts

```lua
Library:SetFont("Ubuntu", "Ubuntu", "Ubuntu")
-- (normal, bold, medium)
```

Available: Gotham, Arial, SourceSans, Ubuntu, Roboto, Code, Cartoon, SciFi, Fantasy, Arcade, Bangers, Bodoni, DenkOne, FredokaOne, Jura, LuckiestGuy, Merriweather, Michroma, Nunito, Oswald, Sarpanch, TitilliumWeb, Zekron, and more (39 total).

---

## Icons

Register icons by name and use them anywhere:

```lua
Library:RegisterIcon("custom", "rbxassetid://123456789")

Section:CreateButton({ Name = "Custom", Icon = "custom" })
```

Built-in icons: `home`, `settings`, `user`, `star`, `play`, `pause`, `search`, `close`, `check`, `plus`, `heart`, `music`, `volume`, `key`, `lock`, `unlock`, `info`, `warning`, `error`, `refresh`, `trash`, `copy`, `link`, `code`, `paint`, `sliders`, `list`, `filter`, `grid`, `eye`, `sun`, `moon`.

---

## Key System

The library ships with an optional key system. **You configure it** — the library just provides the infrastructure.

```lua
local Window = Library:CreateWindow({
    Key = {
        Enabled = true,
        Title = "Key System",
        Description = "Get your key at the link below",
        Link = "https://your-own-site.com/key",        -- your link
        LinkLabel = "Get Key",
        KeyFile = "library_key.json",
        UseHubKey = false,

        -- Option A: local validation (pure Lua)
        Validate = function(key, hwid)
            return key == "YOUR_KEY_HERE"
        end,

        -- Option B: remote validation (your own API)
        RemoteValidate = "https://your-own-api.com/validate",

        -- Option C: log attempts to your Discord webhook
        Webhook = {
            Enabled = true,
            Url = "https://discord.com/api/webhooks/YOUR_WEBHOOK_HERE"
        }
    }
})
```

**You can use any combination** of the three options above. If you don't want a key system at all, just omit the `Key` table.

If you use `RemoteValidate`, your API should respond with:

```json
{ "valid": true, "plan": "pro", "expires": "2026-12-31" }
```

---

## HWID & Security

### Get HWID

```lua
local hwid = Library:GetHWID()            -- raw
local hashed = Library:GetHashedHWID()    -- SHA-256 hash
```

HWID is automatically detected from the executor. If unavailable, a stable fallback is generated from the user ID.

### Crypto Utilities

```lua
Library.Crypto.SHA256("data")
Library.Crypto.Encrypt("plain", "secret")
Library.Crypto.Decrypt(cipher, "secret")
Library.Crypto.Base64Encode("data")
Library.Crypto.Base64Decode("data")
```

### Encrypted Config Files

```lua
Library.Crypto.SaveEncrypted("config.json", {theme="Dark"}, "password")
local cfg = Library.Crypto.LoadEncrypted("config.json", "password")
```

---

## Blocklist

**You provide the blocklist source** — either a remote URL (pastebin, GitHub raw, your own API) or manage it locally.

```lua
Library:SetBlocklist({
    RemoteUrl = "https://raw.githubusercontent.com/YOUR-USER/YOUR-REPO/main/blocklist.json",
    LocalFile = "library_blocklist.json",
    ByHwid = true,
    ByUserId = true,
    ByKey = false,
    CacheSeconds = 300,
    OnBlocked = function(reason)
        game.Players.LocalPlayer:Kick("Blocked: " .. reason)
    end
})

if not Library.Blocklist:RunCheck() then return end
```

Your remote JSON should be formatted like:

```json
{
    "hwids": ["abc123...", "def456..."],
    "userIds": ["123456789"],
    "keys": ["BANNED-KEY-01"]
}
```

Manage locally:

```lua
Library.Blocklist:Add("hwid", "abc123")
Library.Blocklist:Remove("hwid", "abc123")
Library.Blocklist:IsBlocked("hwid", "abc123")
```

---

## License System

```lua
Library:LoadLicense()

if not Library:IsLicenseValid() then
    Library:Notify({ Title = "License", Text = "Expired", Type = "error" })
    return
end

local plan = Library:GetLicensePlan()   -- "free" | "basic" | "pro" | "premium" | "lifetime"

if Library:HasPlan("pro") then
    -- enable pro features
end
```

---

## Profiles

```lua
local profiles = Library:ListProfiles()

Library:SaveProfile("MySetup", { theme = "Dark", volume = 0.5 })
local data = Library:LoadProfile("MySetup")
Library:DeleteProfile("MySetup")
```

### Import / Export

```lua
local encoded = Library:ExportConfig({ theme = "Neon", volume = 0.8 })
-- clipboard is automatically filled

local restored = Library:ImportConfig(encoded)
```

---

## Macros

```lua
Library:StartMacroRecording("MyMacro")
Library:AddMacroStep({ type = "wait", time = 0.5 })
Library:AddMacroStep({ type = "callback", fn = function() print("hi") end })
Library:StopMacroRecording()

Library:LoadMacros()
Library:PlayMacro("MyMacro")
```

---

## Notifications

### Notify

```lua
Library:Notify({
    Title = "Success",
    Text = "Operation completed",
    Type = "success",     -- info | success | warning | error
    Duration = 4,
    Image = "rbxassetid://123456789"   -- optional
})
```

### Toast

```lua
Library:Toast({ Text = "Saved!", Type = "success", Duration = 2 })
```

### Snackbar

```lua
Library:Snackbar({
    Text = "Config applied",
    Type = "success",
    Duration = 3,
    Action = {
        Text = "Undo",
        Callback = function() end
    }
})
```

### Confirm & Prompt

```lua
if Library:Confirm({ Title = "Are you sure?", Description = "This cannot be undone" }) then
    -- yes
end

local text = Library:Prompt({ Title = "Enter name", Placeholder = "..." })
```

---

## Widgets

```lua
Library:AddFPSWidget()
Library:AddPingWidget()
Library:AddMemoryWidget()
Library:AddClockWidget()

-- Custom
Library:AddWidget({
    Id = "mywidget",
    Name = "Custom",
    Icon = "S",
    Color = Color3.fromRGB(148, 132, 232),
    Interval = 1,
    OnUpdate = function() return tostring(os.time()) end
})
```

---

## Effects & Transitions

### Effects

```lua
Library:PlayEffect("Confetti", parentFrame, { Count = 30 })
Library:PlayEffect("Sparkles", player.Character.HumanoidRootPart, { World3D = true })
```

Built-in: `Confetti`, `Sparkles`, `Fire`, `Snow`, `Stars`, `Bubbles`, `Hearts`, `Lightning`, `Rain`, `Dust`, `Orbs`, `Sparks`.

### Transitions

```lua
Library:PlayTransition("ScalePop", someFrame, "in")
```

Built-in: `Fade`, `SlideLeft`, `SlideRight`, `ScalePop`, `ScaleSquish`, `RotateIn`, `BounceIn`, `ZoomIn`.

### Register Custom

```lua
Library:RegisterEffect("MyEffect", { minS=4, maxS=8, dur=2, color=Color3.new(1,1,1) })
Library:RegisterTransition("MyTransition", { dur=0.5, style=Enum.EasingStyle.Quart, dir=Enum.EasingDirection.Out })
```

---

## Sounds

Bind sound asset IDs to library events. **You provide the IDs** — the library ships with sensible defaults.

```lua
Library:SetSounds({
    click = "rbxassetid://6895079853",
    hover = "",
    success = "rbxassetid://6895082385",
    error = "rbxassetid://6895079853",
    open = "",
    close = "",
    enabled = true,
    volume = 0.5,
    silent = false
})
```

Sounds play automatically on built-in interactions if configured.

---

## Utilities

```lua
-- HTTP
Library.Util.HttpGet(url)
Library.Util.HttpPost(url, body)

-- JSON
Library.Util.JsonRead("file.json", default)
Library.Util.JsonWrite("file.json", data)

-- Color
Library.Util.HexToColor("#FFFFFF")
Library.Util.ColorToHex(Color3.new(1,1,1))
```

### UI Scale

```lua
Library:SetUIScale(1.2)             -- global
Library:SetUIScale(1.5, "window")   -- per window
Library:GetUIScale("window")
```

### Streamer Mode

```lua
Library:SetStreamerMode(true)
```

---

## Mobile Support

The library automatically detects touch-only devices and adjusts:

- Tap instead of hover
- Larger hit areas for buttons
- Optimized layout spacing
- Mobile toggle key hint in the status bar

No additional configuration required.

---

## For Library Users

This is a **library**, not a hub. It provides UI, systems, and components — but no ready-made scripts.

### What you configure

Everything that connects to *your* infrastructure is up to you:

| Feature | What you provide |
|---|---|
| **Key System** | Your own key site link, validation logic or API, and/or your Discord webhook |
| **Remote Validation** | Your own API endpoint |
| **Blocklist** | Your own remote JSON URL (or manage locally) |
| **Webhook Logging** | Your own Discord webhook URL |
| **Sounds** | Your own asset IDs (or leave the defaults) |
| **Themes / Fonts** | Your own preferences |
| **Icons** | Your own image asset IDs |

### What the library provides

- All UI rendering and animations
- Component logic (toggles, sliders, dropdowns, etc.)
- Crypto utilities (SHA-256, XOR, Base64)
- HWID detection and hashing
- Local storage helpers (JSON read/write)
- Platform detection
- Everything else that doesn't depend on your infrastructure

### Example — building a hub

```lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/USER/REPO/main/library.lua"))()

local Window = Library:CreateWindow({
    Name = "My Awesome Hub",
    Theme = "Cyberpunk",
    Key = {
        Enabled = true,
        Link = "https://my-hub.com/key",                 -- your site
        Validate = function(k) return k == "ABC123" end, -- your logic
        Webhook = { Enabled = true, Url = "https://discord.com/api/webhooks/YOUR_WEBHOOK" }
    }
})

local Main = Window:CreateTab("Main", "home")
local Actions = Main:CreateSection("Actions")

Actions:CreateButton({
    Name = "Do Something",
    Callback = function()
        -- your code here
    end
})
```

The library handles everything visual and structural. Your hub only needs to define what each button actually does.

---

## FAQ

**Q: Does this work on every executor?**
A: It works on any executor supporting `loadstring`, `game:HttpGet`, and `Instance.new`. Tested on Synapse X, Krnl, Fluxus, SirHurt, and Sentinel.

**Q: Can I use it commercially?**
A: Yes — MIT license, use however you like. Attribution appreciated but not required.

**Q: Does it work on mobile?**
A: Yes, with automatic platform detection and touch-optimized layout.

**Q: How do I update?**
A: Just re-fetch the loadstring. The library version is shown in the status bar.

**Q: Can I hide the default keybind?**
A: Yes — set `ToggleKeys = {}` in window config.

**Q: Does it conflict with other scripts?**
A: No. The library uses random names for its ScreenGuis to avoid collisions with other hubs.

**Q: Do I need a key system?**
A: No. It's optional. Skip the `Key` table in window config if you don't want one.

**Q: Do I need a Discord webhook?**
A: No. It's optional logging. Only enable it if you have your own webhook URL.

**Q: Can I remove parts I don't use?**
A: Yes. Every system (key, blocklist, sounds, effects, widgets) is opt-in.

---

## License

MIT License — see [LICENSE](LICENSE) for details.

---

<p align="center">
  Made with care for the Roblox scripting community.
</p>
