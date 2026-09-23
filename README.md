# Library

A modern, fully customizable Roblox UI library — built for developers who want beautiful interfaces without writing UI code from scratch.

## Features

- **Themes** — 6 built-in palettes, animated theme mode, and custom theme support
- **Fonts** — 39 system fonts to choose from
- **Window Modes** — Compact, Normal, and Wide layouts
- **Animations** — Smooth transitions, hover effects, and animated accents
- **Splash Screen** — Customizable loading screen with progress bar
- **Key System** — Local or remote validation with webhook logging
- **HWID Support** — Automatic hardware ID detection and hashing
- **Encryption** — SHA-256, XOR cipher, and Base64 utilities
- **Blocklist** — Local + remote HWID/UserID/Key blocking
- **License System** — Plan tiers (free, basic, pro, premium, lifetime)
- **Profiles** — Save, load, delete, and switch configurations
- **Macros** — Record and replay action sequences
- **Widgets** — FPS, ping, memory, clock, and custom widgets
- **Notifications** — Toast, Snackbar, and full notification system
- **Effects & Transitions** — 2D/3D particle effects and window transitions
- **Sound System** — Configurable sounds for every event
- **UI Scale** — Global and per-menu scaling
- **Snap to Edge** — Auto-align windows to screen borders
- **Mobile Support** — Touch-friendly layout and controls

## Components

Button, Toggle, Slider, RangeSlider, Input, Label, Paragraph, Divider, Dropdown, MultiSelect, ColorPicker, Keybind, Progress, Image, Search, MiniTabs, GlobalSearch, and more.

## Usage

```lua
local Lib = loadstring(game:HttpGet("https://raw.githubusercontent.com/USER/REPO/main/lib.lua"))()

local Window = Lib:CreateWindow({
    Name = "My Hub",
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
        Lib:Notify({ Title = "Success", Text = "It works!", Type = "success" })
    end
})

Section:CreateToggle({ Name = "Feature", Callback = function(v) end })
Section:CreateSlider({ Name = "Volume", Min = 0, Max = 100, Default = 50 })
Configuration
Every part of the library is configurable through the CreateWindow options — theme, fonts, key system, blocklist, sounds, animations, layout, and more. Nothing is forced; enable only what you need.

Status
Actively developed. New components and features are added regularly.

License
MIT
