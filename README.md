# Pomidor

A minimal, native macOS menu bar Pomodoro timer built with Swift and SwiftUI.

Pomidor lives in your menu bar — no Dock icon, no clutter. Just a clean timer that helps you focus.

## Requirements

- macOS 15 (Sequoia) or later
- Xcode 16 or later
- [XcodeGen](https://github.com/yonaskolb/XcodeGen) (`brew install xcodegen`)

## Build and install from source

```bash
make build
```

This generates the Xcode project and produces a Release build. Copy the app into Applications:

```bash
cp -R ~/Library/Developer/Xcode/DerivedData/Pomidor-*/Build/Products/Release/Pomidor.app /Applications/
```

Launch **Pomidor** from Applications. The timer appears in the menu bar.

Other targets:

```bash
make run            # build, then open the Release app
make debug          # Debug configuration
make generate && open Pomidor.xcodeproj   # open in Xcode
make clean          # remove build artifacts
```

`make distribution` additionally packages the app as a zip and DMG in `dist/` (requires `brew install create-dmg`).

## Features

- **Menu bar native** — runs entirely from the status bar, hidden from the Dock
- **Pomodoro workflow** — 25 min work / 5 min short break / 15 min long break with session tracking
- **Visual progress ring** — animated circular indicator with color-coded sessions
- **Native notifications** — macOS alerts with sound when sessions complete
- **Customizable** — adjust all durations, auto-start behavior, and notification preferences
- **Launch at login** — optional, via the system Login Items API
- **Offline** — no network access, accounts, analytics, or auto-updates
- **Lightweight** — pure Swift + SwiftUI, zero external dependencies

## Project structure

```
Pomidor/
├── App/
│   ├── PomidorApp.swift              # Entry point and app delegate
│   └── StatusItemManager.swift       # Menu bar item and popover
├── Models/
│   ├── TimerState.swift              # Session types and timer phases
│   └── PomidorSettings.swift         # Persisted user preferences
├── Services/
│   ├── TimerManager.swift            # Core timer engine (@Observable)
│   ├── NotificationManager.swift     # macOS notification delivery
│   ├── SoundManager.swift            # Completion sounds
│   └── LaunchAtLoginManager.swift    # Login item registration
├── Views/
│   ├── TimerView.swift               # Main popover UI
│   ├── SettingsView.swift            # Preferences
│   └── Components/
│       ├── CircularProgressView.swift
│       ├── TimerControls.swift
│       └── SessionIndicator.swift
└── Theme/PomidorTheme.swift          # Design tokens
```

## Tech stack

| Layer | Choice |
|-------|--------|
| Language | Swift 5.9+ |
| UI | SwiftUI in an AppKit `NSStatusItem` popover |
| State | @Observable macro |
| Persistence | @AppStorage / UserDefaults |
| Notifications | UserNotifications framework |
| Build | XcodeGen + xcodebuild |

## License

MIT
