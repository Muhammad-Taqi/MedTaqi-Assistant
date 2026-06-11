# MedTaqi Assistant — iOS App Build Guide

## What's Inside This ZIP
```
MedTaqi_iOS/
├── MedTaqiAssistant.xcodeproj/
│   ├── project.pbxproj              ← Full Xcode project config
│   └── project.xcworkspace/
├── MedTaqiAssistant/
│   ├── AppDelegate.swift            ← App entry point
│   ├── ViewController.swift         ← WKWebView wrapper
│   ├── Info.plist                   ← Permissions & app config
│   ├── Assets.xcassets/
│   │   ├── AppIcon.appiconset/      ← Your logo (all iOS sizes)
│   │   └── AccentColor.colorset/
│   ├── Base.lproj/
│   │   └── LaunchScreen.storyboard  ← Splash screen with your logo
│   └── www/
│       └── index.html               ← Your complete MedTaqi app
└── README.md
```

---

## BUILD METHOD 1 — Xcode on Mac (Official, Required for App Store)

### Requirements
- **Mac computer** (macOS 13 Ventura or later)
- **Xcode 15+** — free from Mac App Store: https://apps.apple.com/app/xcode/id497799835
- Apple ID (free) for device testing — no paid account needed for personal use

### Steps

1. **Open the project**
   - Double-click `MedTaqiAssistant.xcodeproj`
   - OR open Xcode → File → Open → select the `.xcodeproj` file

2. **Select your target**
   - In the left panel, click the blue `MedTaqiAssistant` project icon
   - Under "Targets" → `MedTaqiAssistant`
   - In "Signing & Capabilities" tab:
     - Check ✅ "Automatically manage signing"
     - Set "Team" to your Apple ID (add it under Xcode → Settings → Accounts)

3. **Run on Simulator** (no Apple account needed)
   - Top bar: select "iPhone 15" from the device menu
   - Press ▶ Run (Cmd+R)
   - App will launch in the iOS Simulator

4. **Run on Real iPhone**
   - Connect iPhone via USB → Trust the computer
   - Select your iPhone from the device menu
   - Press ▶ Run — Xcode installs it directly

5. **Build IPA for distribution**
   - Product → Archive
   - Distribute App → choose method (Ad Hoc / App Store)

---

## BUILD METHOD 2 — GitHub Actions (No Mac Needed for IPA)

Push this folder to GitHub, add this workflow:

```yaml
# .github/workflows/ios.yml
name: Build iOS IPA
on: [push]
jobs:
  build:
    runs-on: macos-14
    steps:
      - uses: actions/checkout@v4
      - name: Build
        run: |
          cd MedTaqi_iOS
          xcodebuild \
            -project MedTaqiAssistant.xcodeproj \
            -scheme MedTaqiAssistant \
            -sdk iphonesimulator \
            -configuration Debug \
            build
      - uses: actions/upload-artifact@v4
        with:
          name: MedTaqi-iOS-Build
          path: ~/Library/Developer/Xcode/DerivedData
```

---

## BUILD METHOD 3 — Online Services (No Mac Required)

These services build iOS apps in the cloud:

| Service | Free Tier | URL |
|---------|-----------|-----|
| **Codemagic** | 500 min/month free | https://codemagic.io |
| **Bitrise** | Free hobby plan | https://bitrise.io |
| **AppCircle** | Free starter | https://appcircle.io |

**Codemagic Quick Start:**
1. Sign up at codemagic.io with GitHub
2. Upload/push this project
3. Select "Xcode" → configure → Build
4. Download the `.ipa` artifact

---

## INSTALL ON iPhone WITHOUT APP STORE

### Method A — AltStore (Free, No Jailbreak)
1. Install AltStore on your Mac: https://altstore.io
2. Install AltStore on your iPhone via AltServer
3. Drag the `.ipa` → AltStore on iPhone
4. Refresh every 7 days (free Apple ID limit)

### Method B — Sideloadly (Free)
1. Download: https://sideloadly.io
2. Connect iPhone + open Sideloadly
3. Drag `.ipa` → Sign with Apple ID → Install

### Method C — TestFlight (For sharing with others)
- Requires paid Apple Developer account ($99/year)
- Upload via App Store Connect → invite testers

---

## APP FEATURES ENABLED
✅ WKWebView (modern, fast, secure)
✅ Camera access for medical report scanning
✅ Photo library access for image uploads
✅ JavaScript fully enabled
✅ LocalStorage / DOM storage
✅ Fullscreen dark theme (#05080f)
✅ All iOS icon sizes from your MedTaqi logo
✅ Dark status bar (white text)
✅ Portrait locked (landscape for iPad)
✅ Back navigation support
✅ Alert / Confirm / Prompt dialogs
✅ Supports iOS 15.0+
✅ iPhone + iPad (Universal)

---

## App Info
- Bundle ID: `com.medtaqi.assistant`
- Version: 1.0
- Min iOS: 15.0
- Swift: 5.0
- Xcode compatibility: 15+
