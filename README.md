# Windows 11 Order of Business
> [!IMPORTANT]
> This guide assumes you can navigate Windows using menu interfaces and know what adapters your PC is using. Check [here](#afterthought) for Q&A.

| Section | Subsection | Description |
|--------|------------|-------------|
| [I. Preparations](#i-preparations) | | Initial preparations before system changes. |
| [II. System modifications](#ii-system-modifications) | [1. Major tweaks](#1-major-tweaks) | Tweak system settings. |
|  | [2. Minor tweaks](#2-minor-tweaks) | Disable reserved bandwidth, bufferless tracking, share tray, and enable `Win + V`/`;`/`.`. |
|  | [3. Disable unnecessary services](#3-disable-unnecessary-services) |  |
|  | [4. Turn off useless Windows Features](#4-turn-off-useless-windows-features) |  |
| [III. Setting things up](#iii-setting-things-up) | [1. Mouse Cursor and Font](#1-mouse-cursor-and-font) |  |
|  | [2. AccentColorizer](#2-accentcolorizer) |  |
|  | [3. File Explorer](#3-file-explorer) | `explorer.exe` configurations. |
|  | [4. Settings](#4-settings) | Activate Windows and `Win + I` configurations. |
|  | [5. Control Panel](#5-control-panel) | `sysdm.cpl`, `intl.cpl`, `powercfg.cpl`, `inetcpl.cpl`, `mmsys.cpl`, and `ncpa.cpl` configurations. |
|  | [6. Device Manager](#6-device-manager) | Disable unused devices and drivers. |
| [IV. Installing software](#iv-installing-software) | |  |
| [V. Configuring software](#v-configuring-software) | |  |
| [VI. Wrapping things up](#vi-wrapping-things-up) | [After installing and configuring apps and software](#after-installing-and-configuring-apps-and-software) | Cleanup. |
|  | [Afterthought](#afterthought) | Q&A |

---

## I. Preparations

After Windows 11 is installed:
- boot into BIOS to enable Fastboot if haven't. I thoroughly recommend exploring other settings to optimize BIOS, provided that you know what you're doing or seek guidance from AI if you're uncertain;
- immediately `Win + I → Windows Update → Check for updates`. You might have to do this once or twice. Also, check `System → Storage → Remove Temporary Files` while you're at it;
- update BIOS by visiting your PC manufacturer's website and drivers via Windows Update, your PC manufacturer's website, or third-party tools like [Snappy Driver Installer](https://sdi-tool.org/download/ "Glenn Delahoy");
- (OPTIONAL) join Windows Insider Program. You get early access to new features, like **text extractor** and **color picker** in `Win + R → snippingtool` and basic **text formatting** options in `Win + R → notepad` as of writing this in June 2025. Don't join if your Windows 11 is Enterprise LTSC/Enterprise IoT LSTC, or you want maximum stability and don't care about feature updates. [🔍︎](https://youtu.be/YQFx6C6SL08 "ThioJoe")

---

## II. System modifications

`Win + R → UserAccountControlSettings` → drag the slider all the way down → OK

### 1. Major tweaks:

**Required:**
- [CrapFixer](https://github.com/builtbybel/CrapFixer/releases "Builtbybel")
- Chris Titus Tech's Windows Utility (Admin PowerShell): `iwr -useb https://christitus.com/win | iex`
  - Tweaks
  - O&O ShutUp10++
- [RyTuneX](https://rayenghanmi.me/rytunex/download.html "Rayen Ghanmi")
- [Winaero Tweaker](https://winaerotweaker.com "Sergey Tkachenko")
  - Windows 11:
    - Disable Background Apps
    - Disable Copilot
    - Remove Windows Spotlight 
  - Appearance: Startup Sound
  - Advanced Appearance Settings:
    - Icons
    - Menus
    - Message Font
    - Statusbar Font
    - System Font
    - Window Title Bars
  - Behavior
    - Ads and Unwanted Apps
    - Disable SmartScreen
    - Disable User Folder Backup to OneDrive
    - Error Reporting
    - Menu Show Delay
    - Show BSOD
    - Disable Smiley
    - Sound for Print Screen key
    - Split Threshold for Svchost
  - Boot and Logon:
    - Boot Options
    - Disable "Let's finish setting up your device" screen
    - Disable Blur on Sign-in Screen
    - Enable User Auto Logon Checkbox
    - Verbose Logon Messages
  - Desktop and Taskbar:
    - Disable Web Search
    - Wallpaper Quality
  - File Explorer:
    - "Do this for all current items" Checkbox
    - Disable Jump Lists
    - Disable Search History
    - Enable Auto Completion
    - Enable Classic Search
    - Enable Recycle Bin for removable drives
    - File Explorer Starting Folder
    - Navigation Pane - Default Items
  - Windows Defender: Windows Security/Defender Tray Icon
  - Privacy: Disable Telemetry
  - Shortcuts:
    - Disable "- Shortcut" Text
    - Shortcut Arrow
- [Wintoys](https://apps.microsoft.com/detail/9P8LTPGCBZXD "Bogdan Pătrăucean")

**Optional:**
- [Sparkle](https://github.com/Parcoil/Sparkle/releases)
- [Winhance](https://winhance.net "Marco du Plessis")
- [WinScript](https://github.com/flick9000/winscript/releases "Francesco")
- [RemoveWindowsAI](https://github.com/zoicware/RemoveWindowsAI)

### 2. Minor tweaks:
- Disable [reserved bandwidth](https://learn.microsoft.com/en-us/answers/questions/2576537/limit-reservable-bandwidth "Microsoft Learn"): 
  - `Win + R → gpedit.msc → Computer Configuration → Administrative Templates → Network → QoS Packet Scheduler → Limit reservable bandwidth → Enable → Bandwidth limit (%): 0`
  - `Win + R → regedit → Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft → New > Key → Psched → New > DWORD (32-bit) Value → NonBestEffortLimit`
- Disable [bufferless tracking](https://learn.microsoft.com/en-us/windows-hardware/drivers/network/net-buffer-list-structure "Microsoft Learn"): `Win + R → regedit → Computer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NDIS\Parameters → TrackNblOwner → Value data: 0`
- Disable [Drag Tray](https://x.com/phantomofearth/status/1882917685786538245 "X"): `Win + R → regedit → Computer\HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\FeatureManagement\Overrides → New > Key → 14 → New > Key → 3895955085 → New > DWORD (32-bit) Value`
  - `EnabledState → 1`
  - `EnabledStateOptions → 1`
> [!NOTE] You can disable Dray Tray in Settings. [🔍︎](https://youtu.be/LUtEYUz5NCA?t=39)

- Remove [startup delays](https://youtu.be/V7AuHBZsOj0?t=257 "ThioJoe"): `Win + R → regedit → Computer\HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer → New > Key → Serialize → New > DWORD (32-bit) Value`
  - `StartupDelayInMSec → 1`
  - `WaitForIdleState → 0`
- Enable clipboard history:
  - `Win + R → regedit → Computer\HKEY_CURRENT_USER\Software\Microsoft\Clipboard → EnableClipboardHistory → 1`
  - `Win + R → gpedit.msc → Computer Configuration → Administrative Templates → System → OS Policies → Allow Clipboard History → Enable`

### 3. Disable unnecessary services
- `Win + R → services.msc`
  - ActiveX Installer (AxInstSV)
  - AssignedAccessManager Service
  - AVCTP service `(disable it if you don't intent on using wireless technology like Bluetooth)`
  - BitLocker Drive Encryption Service `(depends, don't disable it if you actually use BitLocker)`
  - Bluetooth Audio Gateway Service `(disable it if you don't use Bluetooth)`
  - Bluetooth User Support Service `(disable it if you don't use Bluetooth)`
  - Certificate Propagation
  - Connected User Experiences and Telemetry
  - Downloaded Maps Manager
  - Diagnostic Policy Service `(disable it and the 2 below if you don't need to diagnose issues on your PC)`
  - Diagnostic Service Host
  - Diagnostic System Host
  - Distributed Link Tracking Client `(disable it if you are a home user or your computer is not part of a large network domain)`
  - Fax
  - Geolocation Service
  - Hyper-V Data Exchange Service `(disable all Hyper-V services if you don't use a virtual machine)`
  - [...]
  - Hyper-V Volume Shadow Copy Requestor
  - IP Helper `(disable it if you don't use IPv6, visit` [here](https://test-ipv6.com "Jason Fesler") `for validation)`
  - Netlogon
  - Parental Controls
  - Print Spooler `(don't disable it if you have a printer at home and you use it)`
  - Phone Service `(disable if you don't use`[Phone Link](https://microsoft.com/windows/sync-across-your-devices "Microsoft")`)`
  - Remote Access Auto Connection Manager
  - Remote Desktop Configuration
  - Remote Desktop Services
  - Remote Registry
  - Secondary Logon
  - Sensor Service `(disabling it will cause Power & battery in Win + I → System to crash)`
  - SmartCard `(disable it and the 2 below if you don't use smart card)`
  - SmartCard Device Enumeration Service
  - SmartCard Removal Policy
  - SysMain `(disable it if your storage device is HDD, Task Manager → Performance → Disk 0 (C:))`
  - TCP/IP NetBIOS Helper `(disable it if you don't use`[Workgroup](https://wikipedia.org/wiki/Workgroup_(computer_networking) "Wikipedia")`)`
  - Touch Keyboard and Handwriting Panel Service `(disable it if you aren't a digital artist)`
  - WalletService
  - Windows Biometric Service `(disable it if you don't use Windows Hello)`
  - Windows Error Reporting Service
  - Windows Image Acquisition `(disable it if you don't use a scanner or camera)`
  - Windows Insider Service `(disable it if you aren't part of Windows Insider Program)`
  - Windows Mobile Hotspot Service `(disable it if you don't wish to turn your PC into a hotspot)`
  - Windows Search `(disable it to disable the ability to search files via Windows Search)`
  - Xbox Accessory Management Service `(disable it and the 3 below if you don't use Xbox)`
  - Xbox Live Auth Manager
  - Xbox Live Game Save
  - Xbox Live Networking Service

- `Win + R → msconfig → Services → Hide all Microsoft services → Disable all → Apply → OK`

### 4. Turn off useless Windows Features:
`Win + R → optionalfeatures`
- Media Features
- Microsoft Print to PDF
- Remote Differential Compression API Support
- Work Folder Clients

---

## III. Setting things up

### 1. Mouse Cursor and Font
- [Mouse Cursor](⛁/deviantart-jepricreations-cursor)
- [Fonts](⛁/fonts)

### 2. AccentColorizer:  
   - [AccentColorizer](https://github.com/krlvm/AccentColorizer "krlvm")  
   - [AccentColorizer-E11](https://github.com/krlvm/AccentColorizer-E11 "krlvm")

### 3. File Explorer:
  - Configure Quick access
  - Show details pane
  - ⋯ → Options
 
![[June 2025] File Explorer](🀦/[June-2025]-File-Explorer.png)

### 4. Settings:
  - **Activate Windows (Admin PowerShell)**:
  	- `irm https://get.activated.win | iex`
   	- `irm https://massgrave.dev/get | iex`
  - `Win + I`  
	- System
	- Bluetooth & devices
	- Network & internet
	- Personalization
	- Apps
	- Accounts
	- Time & language
	- Gaming
	- Accessibility
	- Privacy & security
	- Windows Update

### 5. Control Panel:
  - **System Properties**: `Win + R → sysdm.cpl`
  - **Region**: `Win + R → intl.cpl → Formats`
  - **Power Options**: `Win + R → powercfg.cpl`
  - **Internet Properties**: `Win + R → inetcpl.cpl → Connections → LAN settings →` uncheck `Automatically detect settings`

  - **Sound**: `Win + R → mmsys.cpl`
     - Communications → When Windows detects communications activities: Do nothing
     - Playback → select the speaker your PC is using as output → Properties:
     	- Spatial sound → Windows Sonic for Headphones
     	- If there's Enhancements, select Bass Boost, Virtual Surround, Loudness Equalization.
     	- If not: `Win + R → devmgmt.msc` → Sound, video and game controllers → right click the speaker your PC is using as output → Disable device → Update driver → Browse my computer for drivers → Let me pick from a list of available drivers on my computer → uncheck Show compatible hardware → Manufacturer: Microsoft → in Model select High Definition Audio Device Version the latest date → Yes → Close → Reboot

  - **Network Connections**: `Win + R → ncpa.cpl` → double click / right click on the network connection you're using (either Ethernet or Wi-Fi) → Properties
	- This connection uses the following items:
		- 🗹 QoS Packet Scheduler
		- 🗹 Internet Protocol Version 4 (TCP/IPv4)
		- 🗹 Internet Protocol Version 6 (TCP/IPv6) `(if you use` [IPv6](https://test-ipv6.com)`)`
	- Internet Protocol Version 4 (TCP/IPv4) → Properties → Use the following DNS server addresses: Preferred DNS server is **1.1.1.1** and Alternate DNS server is **1.0.0.1** → Close
	- Connected using: [NETWORK_ADAPTER_NAME] → Configure...
		- Power Management → uncheck Allow the computer to turn off this device to save power
		- Advanced → screenshot the window and ask AI which ones to fine-tune for network performance (or visit [this one](https://khorvie.tech/wifinic "Khorvie") or [that one](https://khorvie.tech/ethernetnic "Khorvie") for instructions) → OK

### 6. Device Manager:
`Win + R → devmgmt.msc`
  - Audio inputs and outputs: disable the ones you don't use
  - Network adapters:
    - disable the ones you don't use like Ethernet for many people
    - right click on the network adapter you use → Properties → Power Management → uncheck Allow the computer to turn off this device to save power
    - disable Microsoft Kernel Debug Network Adapter `(for kernel debugging like BSOD)`
  - Software devices: disable Microsoft GS Wavetable Synth `(an old, software-based MIDI player from the 90s)`
  - Sound, video and game controllers: disable the ones you don't use
  - System Devices: disable
    - System speaker `(used for diagnostics in BIOS)`
    - Remote Desktop Device Redirector Bus `(allows local devices like printers to be used remotely)`
    - NDIS Virtual Network Adapter Enumerator `(for VMs)`
    - Microsoft Hyper-V Virtualization Infrastructure Driver `(for VMs)`

---

## IV. Installing software

> [!NOTE]
> - Install UniGetUI in Microsoft Store. If your Windows 11 is Enterprise LTSC/Enterprise IoT LSTC, run this command in Admin PowerShell to install Microsoft Store: `wsreset -i`
> - All applications and software listed below are available for download via UniGetUI, Microsoft Store, or online through links. Ones without links are from Microsoft Store and can be downloaded from itself or UniGetUI.
> - Not all of them listed here have to be downloaded, as it's up to your decision.

#‎ 
- [Main & Additional Browser](https://youtu.be/YrxhVA5NVQ4?si=qIAoQn81kIaUU1bM "Juxtopposed"): [🔍︎](#afterthought "Afterthought")
	- Chromium-based: [Brave](https://brave.com/download) / [Helium](https://helium.computer) / [Vivaldi](https://vivaldi.com/download) / ...
	- Firefox fork: [Floorp](https:/floorp.app/en-US/download) / [Librewolf](https://librewolf.net/installation/windows) / [Zen Browser](https://zen-browser.app/download) / ...

A
- [AB Download Manager](https://abdownloadmanager.com)
- [Audacity](https://audacityteam.org/download/windows)

B
- [BCUninstaller](https://sourceforge.net/projects/bulk-crap-uninstaller)
- [Blip](https://blip.net/download/windows)

C
- Calculator
- [Camomile App](https://camomileapp.com)
- [Context Menu Manager](https://github.com/BluePointLilac/ContextMenuManager/releases)

D
- [DefenderUI](https://cyberlock.global/DefenderUI.aspx)
- [Discord](https://discord.com/download)
	- [Vencord](https://vencord.dev/download)
	- [BetterDiscord](https://betterdiscord.app/themes)
- Dropshelf

E
- Energy Star X
- [Everything](https://voidtools.com/downloads)

F
- [File Converter](https://file-converter.io/download.html)
- FluentFlyout
- [FxSound](https://fxsound.com/download)

G
- [GeoGebra Classic](https://geogebra.org/download)
- [GIMP](https://gimp.org/downloads)
	- [Resynthesizer](https://gimpchat.com/viewtopic.php?f=7&t=21535#p294979)

I
- [Icaros](https://github.com/Xanashi/Icaros/releases)
- [Image Glass](https://imageglass.org/releases)
	- [WinUI3 Dark](https://imageglass.org/theme/winui3-dark-mizan-53)

K
- [Kdenlive](https://kdenlive.org/download)

M
- [Microsoft Teams](https://microsoft.com/en-us/microsoft-teams/download-app)
- [MinGW (VS Code)](https://code.visualstudio.com/docs/cpp/config-mingw)
- [MKVToolNix](https://mkvtoolnix.download/downloads.html#windows)

N
- NanaZip
- [Nilesoft Shell](https://nilesoft.org/download)
- Notepad

O
- [Office 2021](https://microsoft.com/en-us/microsoft-365/download-office#download) [🔍︎](#afterthought "Afterthought")
- OnionMedia

P
- Paint
- [PDF24 Creator](https://tools.pdf24.org/en/creator#download) [🔍︎](#afterthought "Afterthought")
- [PowerToys](https://github.com/microsoft/PowerToys/releases)
	- [EverythingPowerToys](https://github.com/lin-ycv/EverythingPowerToys/releases)
- [Proton Pass](https://proton.me/pass/download)
- [Proton VPN](https://protonvpn.com/download)
- Python: `(installing either Anaconda or Python Software Foundation provides the same Python environment)`
	- [Anaconda](https://anaconda.com/download)
	- [Python Software Foundation](https://python.org)

Q
- [qBittorrent](https://qbittorrent.org/download)
	- [ayuDark](https://github.com/maboroshin/qBittorrentDarktheme/releases)
- [QuickCPU](https://coderbag.com/product/quickcpu)

R
- Radiograph

S
- Screenbox
- [SDelete](https://learn.microsoft.com/en-us/sysinternals/downloads/sdelete)
	- [SDelete Gui](https://github.com/Tulpep/SDelete-Gui/releases)
- [Send to Kindle](https://amazon.com/sendtokindle/pc)
- Skyline Weather
- Snipping Tool
- Sound Recorder

T
- [TI Connect CE](https://education.ti.com/en/software/update/84-ce-software-update)
- TranslucentTB

U
- [Upscayl](https://upscayl.org/download)

V
- [ValiDrive](https://grc.com/validrive.htm)
- [Visual Studio Code](https://code.visualstudio.com/download)

W
- [Windhawk](https://windhawk.net)
- [WinfrGUI](https://winfr.org/download.html)
- [WizTree](https://diskanalyzer.com/download)
- [Writing Tools](https://github.com/theJayTea/WritingTools)

X
- [X-Mouse Button Control](https://xmousebuttoncontrol.com/download-for-windows)

Y
- [Youtube Music Desktop App](https://ytmdesktop.app)

Z
- [Zalo](https://zalo.me/pc)

---

## V. Configuring software

> [!NOTE]
> Apps and software not listed here aren't important to immediately configure, or their settings don't have much to configure.

#‎ 
- [Main & Additional Browser]: sign in to restore add-ons, bookmarks, and home page shortcuts `(NOTE: this process is only for Firefox fork)`
	- `about:settings`
	- `about:addons` → Themes
	- `about:addons` → Extensions
	- `about:home`
	- Customize Toolbar...
	- Bookmarks Toolbar → Open All in Tabs `(to load all favicons in bookmarks)`
	- Ctrl + H → View ⌵ → By Last Visited
	- `chrome://flags` (Chromium-based) / `about:config` (Firefox fork) [🔍︎](⛁/BrowserModification.md "Browser Modification")
	- [Bypass Paywalls Clean](https://gitflic.ru/project/magnolia1234/bpc_uploads "magnolia1234")

![[June 2025] Floorp Homepage](🀦/[Jan-2026]-Floorp-Homepage.png)

A
- AB Download Manager: Tools → Settings `(remember to also configure the browser extension's settings for it)`

B
- BCUninstaller: Tools
	- Open Startup Manager
 	- Clean up "Program Files" folders...

C
- Camomile App: Settings

D
- Discord:
	- Themes: [ClearVision](https://betterdiscord.app/theme/ClearVision "BetterDiscord"); [EmojiReplace](https://betterdiscord.app/theme/EmojiReplace "BetterDiscord"); [RadialStatus](https://betterdiscord.app/theme/RadialStatus "BetterDiscord")
 	- Plugins:
		- AlwaysAnimate
		- AlwaysExpandRoles
		- AlwaysTrust
		- BetterFolders
		- BetterGifAltText
		- BetterNotesBox
		- BetterRoleContext
		- BetterSessions
		- BetterSettings
		- BetterUploadButton
		- BlurNSFW
		- ClearURLs
		- CopyFileContents
		- CopyUserURLs
		- FakeNitro
		- FavoriteEmojiFirst
		- FixImagesQuality
		- ForceOwnerCrown
		- FriendsSince
		- FullSearchContext
		- GameActivityToggle
		- ImageZoom
		- ImplicitRelationships
		- InvisibleChat
		- MemberCount
		- MentionAvatars
		- MessageClickActions
		- MessageLatency
		- MessageLinkEmbeds
		- MutualGroupDMs
		- NoBlockedMessages
		- NoF1
		- NoMaskedUrlPaste
		- PermissionsViewer
		- PictureInPicture
		- PlatformIndicators
		- PreviewMessage
		- QuickMention
		- QuickReply
		- ReadAllNotificationsButton
		- RevealAllSpoilers
		- ReverseImageSearch
		- ReviewDB
		- RoleColorEverywhere
		- SendTimestamps
		- ServerInfo
		- ServerListIndicators
		- ShowAllMessageButtons
		- ShowConnections
		- ShowHiddenChannels
		- ShowHiddenThings
		- ShowMeYourName
		- ShowTimeoutDuration
		- SilentMessageToggle
		- SilentTyping
		- SortFriendRequests
		- StartupTimings
		- Summaries
		- SuperReactionTweaks
		- Translate
		- TimeBarAllActivities
		- TypingIndicator
		- TypingTweaks
		- UserMessagesPronouns
		- ValidReply
		- ValidUser
		- ViewIcons
		- VoiceChatDoubleClick
		- WhoReacted

E
- Everything: Tools → Options...

F
- FxSound: ☰ → Settings

G
- GIMP:
![[June 2025] GIMP](🀦/[June-2025]-GIMP.png)

	- Resynthesizer:
```
C:\Users\[NAME]\AppData\Roaming\GIMP\3.0\plug-ins
C:\Users\[NAME]\AppData\Roaming\GIMP\3.0\scripts
```

I
- ImageGlass:
![🀦 → [June 2025] ImageGlass](🀦/[June-2025]-ImageGlass.png)

N
- Nilesoft Shell: `C:\Program Files\Nilesoft Shell\imports\theme.nss`
```
theme
{
	name = "modern"
	view = view.medium
	dark = true
	background
	{
		color = default
		opacity = 15
		effect = [3, default, 30]
	}
	image.align = 2
	border
	{
		enabled = true
		size = 1
		color = #808080
		opacity = 30
		radius = 2
	}
	image
	{
		enabled = true
		color = [image.color1, color.accent, image.color3]
		scale = true
	}
}
```

O
- Office 2021: activate it through Administrator PowerShell
	- `irm https://get.activated.win | iex`
	- `irm https://massgrave.dev/get | iex`
	- Account → Account Privacy: Manage Settings
	- Account → Microsoft 365 and Office Updates → Update Options → Update Now
	- Options

![[June 2025] MS Word](🀦/[June-2025]-MS-Word.png)

P
- PowerToys:
	- Advanced Paste
	- Always On Top
	- PowerToys Run:
		- Program
		- Windows System Commands
		- Windows settings
		- Everything
	- PowerRename

S
- Skyline Weather: `Win + I → Personalization → Lock screen status` → Weather
- StartAllBack: disable start menu and taskbar

V
- Visual Studio Code: sign into Microsoft account and open project folder

W
- Windhawk:
	- Better file sizes in Explorer details
	- Click on empty taskbar space
	- Cycle through taskbar windows on click
	- Taskbar auto-hide speed
	- Taskbar minimize/restore on scroll
	- Taskbar Thumbnail Reorder
	- Taskbar Thumbnail Size
	- Taskbar tray system icon tweaks
 	- Translucent Windows
	- Windows 11 Styler

⚬ File Explorer

⚬ Start Menu `(unless you have the `[new start menu](https://www.theverge.com/news/683818/microsoft-windows-11-new-start-menu-testing-dev-channel)`, don't apply this code)`
```
{
  "controlStyles[0].target": "Windows.UI.Xaml.Controls.Grid#UndockedRoot",
  "controlStyles[0].styles[0]": "Visibility=Visible",
  "controlStyles[0].styles[1]": "Width=450",
  "controlStyles[0].styles[2]": "Margin=200,-10,0,0",
  "controlStyles[1].target": "Windows.UI.Xaml.Controls.Grid#AllAppsRoot",
  "controlStyles[1].styles[0]": "Visibility=Visible",
  "controlStyles[1].styles[1]": "Width=290",
  "controlStyles[1].styles[2]": "Transform3D:=<CompositeTransform3D TranslateX=\"-1100\" />",
  "controlStyles[1].styles[3]": "Margin=175,0,-220,-49",
  "controlStyles[2].target": "Windows.UI.Xaml.Controls.Button#CloseAllAppsButton",
  "controlStyles[2].styles[0]": "Visibility=Collapsed",
  "controlStyles[3].target": "StartDocked.StartSizingFrame",
  "controlStyles[3].styles[0]": "MinWidth=650",
  "controlStyles[3].styles[1]": "MaxWidth=650",
  "controlStyles[3].styles[2]": "MaxHeight=700",
  "controlStyles[4].target": "Windows.UI.Xaml.Controls.Grid#ShowMoreSuggestions",
  "controlStyles[4].styles[0]": "Visibility=Visible",
  "controlStyles[5].target": "Windows.UI.Xaml.Controls.Button#ShowAllAppsButton",
  "controlStyles[5].styles[0]": "Visibility=Collapsed",
  "controlStyles[6].target": "Windows.UI.Xaml.Controls.GridView#RecommendedList > Windows.UI.Xaml.Controls.Border > Windows.UI.Xaml.Controls.ScrollViewer#ScrollViewer > Windows.UI.Xaml.Controls.Border#Root > Windows.UI.Xaml.Controls.Grid > Windows.UI.Xaml.Controls.ScrollContentPresenter#ScrollContentPresenter > Windows.UI.Xaml.Controls.ItemsPresenter > Windows.UI.Xaml.Controls.ItemsWrapGrid > Windows.UI.Xaml.Controls.GridViewItem",
  "controlStyles[6].styles[0]": "MaxWidth=190",
  "controlStyles[6].styles[1]": "MinWidth=190",
  "controlStyles[6].styles[2]": "Margin=0,0,0,0",
  "controlStyles[7].target": "StartDocked.AllAppsGridListView#AppsList",
  "controlStyles[7].styles[0]": "Padding=90,3,6,16",
  "controlStyles[8].target": "Windows.UI.Xaml.Controls.Grid#AllAppsPaneHeader",
  "controlStyles[8].styles[0]": "Margin=97,-10,0,0",
  "controlStyles[9].target": "Windows.UI.Xaml.Controls.Grid#SuggestionsParentContainer",
  "controlStyles[9].styles[0]": "Visibility=Visible",
  "controlStyles[10].target": "StartDocked.NavigationPaneView#NavigationPane",
  "controlStyles[10].styles[0]": "FlowDirection=0",
  "controlStyles[10].styles[1]": "Margin=30,0,30,0",
  "controlStyles[11].target": "StartDocked.PowerOptionsView",
  "controlStyles[11].styles[0]": "Margin=0,-1085,-7,0",
  "controlStyles[11].styles[1]": "CornerRadius=99",
  "controlStyles[12].target": "Windows.UI.Xaml.Controls.ItemsStackPanel",
  "controlStyles[12].styles[0]": "FlowDirection=1",
  "controlStyles[13].target": "Windows.UI.Xaml.Controls.ListViewItem",
  "controlStyles[13].styles[0]": "FlowDirection=0",
  "controlStyles[14].target": "Windows.UI.Xaml.Controls.ItemsStackPanel > Windows.UI.Xaml.Controls.ListViewItem",
  "controlStyles[14].styles[0]": "FlowDirection=0",
  "controlStyles[15].target": "StartDocked.SearchBoxToggleButton#StartMenuSearchBox",
  "controlStyles[15].styles[0]": "Margin=23,-101,23,-514",
  "controlStyles[16].target": "Windows.UI.Xaml.Controls.TextBlock#NoSuggestionsWithoutSettingsLink",
  "controlStyles[16].styles[0]": "Margin=11,0,48,0",
  "controlStyles[17].target": "StartDocked.LauncherFrame > Windows.UI.Xaml.Controls.Grid#RootGrid > Windows.UI.Xaml.Controls.Grid#RootContent > Windows.UI.Xaml.Controls.Grid#MainContent > Windows.UI.Xaml.Controls.Grid#InnerContent > Windows.UI.Xaml.Shapes.Rectangle",
  "controlStyles[17].styles[0]": "Margin=67,7,0,21",
  "controlStyles[18].target": "Windows.UI.Xaml.Controls.SemanticZoom#ZoomControl",
  "controlStyles[18].styles[0]": "IsZoomOutButtonEnabled=true",
  "controlStyles[19].target": "Windows.UI.Xaml.Controls.Button#ZoomOutButton > Windows.UI.Xaml.Controls.ContentPresenter#ContentPresenter > Windows.UI.Xaml.Controls.TextBlock",
  "controlStyles[19].styles[0]": "Text=",
  "controlStyles[20].target": "Windows.UI.Xaml.Controls.Button#ZoomOutButton",
  "controlStyles[20].styles[0]": "Width=28",
  "controlStyles[20].styles[1]": "Height=28",
  "controlStyles[20].styles[2]": "Margin=0,-36,10,0",
  "controlStyles[20].styles[3]": "FontSize=14",
  "controlStyles[20].styles[5]": "VerticalAlignment=0",
  "controlStyles[20].styles[4]": "CornerRadius=4",
  "controlStyles[20].styles[6]": "BorderBrush:=<RevealBorderBrush Color=\"Transparent\" TargetTheme=\"1\" Opacity=\"0.8\"/>",
  "controlStyles[20].styles[7]": "Background:=<RevealBorderBrush Color=\"Transparent\" TargetTheme=\"1\" Opacity=\"0.3\"/>",
  "controlStyles[21].target": "Windows.UI.Xaml.Controls.ListView#ZoomAppsList",
  "controlStyles[21].styles[0]": "Padding=86,0,27,0",
  "controlStyles[22].target": "StartDocked.SearchBoxToggleButton",
  "controlStyles[22].styles[0]": "Height=38",
  "controlStyles[22].styles[1]": "Margin=215,-10,70,30",
  "controlStyles[22].styles[2]": "CornerRadius=20",
  "controlStyles[23].target": "StartMenu.PinnedList",
  "controlStyles[23].styles[0]": "Height=500",
  "controlStyles[24].target": "Windows.UI.Xaml.Controls.TextBlock#PinnedListHeaderText",
  "controlStyles[24].styles[0]": "Margin=-30,0,0,0",
  "controlStyles[25].target": "Windows.UI.Xaml.Controls.Grid#SuggestionsParentContainer",
  "controlStyles[25].styles[0]": "Margin=-20,0,0,0",
  "controlStyles[26].target": "Windows.UI.Xaml.Controls.Grid#TopLevelSuggestionsListHeader",
  "controlStyles[26].styles[0]": "Visibility=Visible",
  "controlStyles[27].target": "Windows.UI.Xaml.Controls.Border#ContentBorder > Windows.UI.Xaml.Controls.Grid#DroppedFlickerWorkaroundWrapper > Border@CommonStates",
  "controlStyles[27].styles[0]": "BorderBrush@Active:=<RevealBorderBrush Color=\"White\" TargetTheme=\"1\" Opacity=\"0.3\"/>",
  "controlStyles[27].styles[1]": "Background:=<RevealBorderBrush Color=\"Transparent\" TargetTheme=\"1\" Opacity=\"0.3\"/>",
  "controlStyles[27].styles[2]": "Margin=1",
  "controlStyles[27].styles[3]": "BorderBrush:=<RevealBorderBrush Color=\"Transparent\" TargetTheme=\"1\" Opacity=\"0.8\"/>",
  "controlStyles[28].target": "Windows.UI.Xaml.Controls.Border#ContentBorder > Windows.UI.Xaml.Controls.Grid#DroppedFlickerWorkaroundWrapper > Border#BackgroundBorder",
  "controlStyles[28].styles[0]": "Background:=<RevealBorderBrush Color=\"Transparent\" TargetTheme=\"0\" Opacity=\".1\"/>\t",
  "controlStyles[28].styles[1]": "Margin=2",
  "controlStyles[29].target": "Windows.UI.Xaml.Controls.TextBlock#PinnedListHeaderText",
  "controlStyles[29].styles[0]": "Visibility=Visible",
  "controlStyles[30].target": "Rectangle[4]",
  "controlStyles[30].styles[0]": "Margin=0,-20,0,0",
  "controlStyles[31].target": "Border#AcrylicBorder",
  "controlStyles[31].styles[0]": "CornerRadius=10",
  "controlStyles[31].styles[1]": "Margin=0",
  "controlStyles[31].styles[2]": "BorderThickness=1",
  "controlStyles[32].target": "Border#AcrylicOverlay",
  "controlStyles[32].styles[0]": "CornerRadius=10",
  "controlStyles[32].styles[1]": "BorderBrush:=<RevealBorderBrush Color=\"Transparent\" TargetTheme=\"1\" Opacity=\"0.8\"/>",
  "controlStyles[32].styles[2]": "BorderThickness=1",
  "controlStyles[32].styles[3]": "Margin=215,75,15,-50",
  "controlStyles[33].target": "Border#DropShadow",
  "controlStyles[33].styles[0]": "CornerRadius=30",
  "controlStyles[33].styles[1]": "Margin=0",
  "controlStyles[34].target": "Border#DropShadowDismissTarget",
  "controlStyles[34].styles[0]": "CornerRadius=30",
  "controlStyles[34].styles[1]": "Margin=0",
  "controlStyles[35].target": "StartDocked.PowerOptionsView > StartDocked.NavigationPaneButton > Grid > Border",
  "controlStyles[35].styles[0]": "CornerRadius=99",
  "controlStyles[35].styles[1]": "Margin=2,3,2,0",
  "controlStyles[36].target": "StartDocked.UserTileView",
  "controlStyles[36].styles[0]": "Margin=-17,-1080,0,0",
  "controlStyles[37].target": "StartDocked.UserTileView > StartDocked.NavigationPaneButton > Grid > Border",
  "controlStyles[37].styles[0]": "Margin=8,0,0,0",
  "controlStyles[37].styles[1]": "CornerRadius=20",
  "controlStyles[38].target": "StartDocked.SearchBoxToggleButton > Grid > Border",
  "controlStyles[38].styles[0]": "Background=#11ffffff",
  "controlStyles[39].target": "StartDocked.LauncherFrame > Grid#RootGrid > Grid#RootContent > Grid#MainContent > Grid#InnerContent > Rectangle",
  "controlStyles[39].styles[0]": "Visibility=Visible",
  "controlStyles[40].target": "StartDocked.NavigationPaneView",
  "controlStyles[40].styles[0]": "Height=50",
  "controlStyles[41].target": "StartDocked.AppListView#NavigationPanePlacesListView",
  "controlStyles[41].styles[0]": "Margin=0,-30,0,0",
  "controlStyles[42].target": "StartDocked.AppListViewItem > Grid",
  "controlStyles[42].styles[0]": "Margin=2",
  "controlStyles[42].styles[1]": "BorderBrush:=<RevealBorderBrush Color=\"Transparent\" TargetTheme=\"1\" Opacity=\"1\"/>",
  "controlStyles[42].styles[2]": "BorderThickness=1",
  "controlStyles[42].styles[3]": "Background:=<RevealBorderBrush Color=\"Transparent\" TargetTheme=\"1\" Opacity=\"0.3\"/>\t",
  "controlStyles[43].target": "StartDocked.AppListViewItem > Grid#ContentBorder@CommonStates",
  "controlStyles[43].styles[0]": "CornerRadius=20",
  "controlStyles[44].target": "MenuFlyoutPresenter",
  "controlStyles[44].styles[0]": "BorderBrush:=<RevealBorderBrush Color=\"Transparent\" TargetTheme=\"1\" Opacity=\"0.8\"/>",
  "controlStyles[44].styles[1]": "BorderThickness=1",
  "controlStyles[45].target": "Windows.UI.Xaml.Controls.FlyoutPresenter[1]",
  "controlStyles[45].styles[0]": "Transform3D:=<CompositeTransform3D TranslateX=\"50\"/>"
}
```
⚬ Taskbar
```
{
  "controlStyles[0].target": "Taskbar.TaskbarFrame#TaskbarFrame",
  "controlStyles[0].styles[0]": "Width=Auto",
  "controlStyles[0].styles[1]": "Height=50",
  "controlStyles[0].styles[2]": "Margin=0,0,0,0",
  "controlStyles[0].styles[3]": "BorderBrush:=<SolidColorBrush Color=\"#808080\" Opacity=\"0.3\" />",
  "controlStyles[0].styles[4]": "BorderThickness=1",
  "controlStyles[1].target": "Taskbar.TaskbarFrame#TaskbarFrame > Grid#RootGrid",
  "controlStyles[1].styles[0]": "Background:=<AcrylicBrush TintColor=\"{ThemeResource SystemChromeAltHighColor}\" TintOpacity=\"0.3\" FallbackColor=\"{ThemeResource SystemChromeLowColor}\" />",
  "controlStyles[1].styles[1]": "Padding=0",
  "controlStyles[1].styles[2]": "CornerRadius=25",
  "controlStyles[1].styles[3]": "BorderThickness=1",
  "controlStyles[1].styles[4]": "BorderBrush:=<SolidColorBrush Color=\"#808080\" Opacity=\"0.3\" />",
  "controlStyles[1].styles[5]": "Margin=5,0,5,5",
  "controlStyles[2].target": "Rectangle#BackgroundFill",
  "controlStyles[2].styles[0]": "Visibility=Visible",
  "controlStyles[2].styles[1]": "BorderBrush:=<SolidColorBrush Color=\"#808080\" Opacity=\"0.3\" />",
  "controlStyles[2].styles[2]": "BorderThickness=2",
  "controlStyles[3].target": "Rectangle#BackgroundStroke",
  "controlStyles[3].styles[0]": "Visibility=Collapsed",
  "controlStyles[4].target": "Taskbar.AugmentedEntryPointButton#AugmentedEntryPointButton > Taskbar.TaskListButtonPanel#ExperienceToggleButtonRootPanel",
  "controlStyles[4].styles[0]": "Margin=0",
  "controlStyles[5].target": "Grid#SystemTrayFrameGrid",
  "controlStyles[5].styles[0]": "Background:=<AcrylicBrush TintColor=\"{ThemeResource SystemChromeHighColor}\" TintOpacity=\"0.3\" FallbackColor=\"{ThemeResource SystemChromeLowColor}\" />",
  "controlStyles[5].styles[1]": "Margin=0,5,10,10",
  "controlStyles[5].styles[2]": "CornerRadius=20",
  "controlStyles[5].styles[3]": "Padding=5",
  "controlStyles[6].target": "SystemTray.ChevronIconView",
  "controlStyles[6].styles[0]": "Padding=0,-1",
  "controlStyles[6].styles[1]": "CornerRadius=5",
  "controlStyles[7].target": "SystemTray.NotifyIconView#NotifyItemIcon",
  "controlStyles[7].styles[0]": "Padding=0,-1",
  "controlStyles[7].styles[1]": "CornerRadius=5",
  "controlStyles[8].target": "SystemTray.OmniButton",
  "controlStyles[8].styles[0]": "Padding=0,-1",
  "controlStyles[8].styles[1]": "CornerRadius=5",
  "controlStyles[9].target": "SystemTray.OmniButton#NotificationCenterButton > Grid > ContentPresenter > ItemsPresenter > StackPanel > ContentPresenter > systemtray:IconView#SystemTrayIcon > Grid",
  "controlStyles[9].styles[0]": "Padding=4,0,4,0",
  "controlStyles[10].target": "SystemTray.IconView#SystemTrayIcon > Grid#ContainerGrid > ContentPresenter#ContentPresenter > Grid#ContentGrid > SystemTray.TextIconContent > Grid#ContainerGrid",
  "controlStyles[10].styles[0]": "Padding=0",
  "controlStyles[11].target": "SystemTray.StackListView#IconStack > ItemsPresenter > StackPanel > ContentPresenter > SystemTray.IconView#SystemTrayIcon",
  "controlStyles[11].styles[0]": "Padding=0",
  "controlStyles[12].target": "SystemTray.Stack#ShowDesktopStack",
  "controlStyles[12].styles[0]": "Margin=0,-4,-12,-4",
  "controlStyles[13].target": "SystemTray.OmniButton#NotificationCenterButton > Grid > ContentPresenter > ItemsPresenter > StackPanel > ContentPresenter > SystemTray.IconView#SystemTrayIcon > Grid > Grid > SystemTray.TextIconContent",
  "controlStyles[13].styles[0]": "Visibility=Visible",
  "controlStyles[14].target": "Taskbar.AugmentedEntryPointButton#AugmentedEntryPointButton > Taskbar.TaskListButtonPanel#ExperienceToggleButtonRootPanel > Border#BackgroundElement@CommonStates",
  "controlStyles[14].styles[0]": "Background:=<AcrylicBrush TintColor=\"{ThemeResource SystemChromeHighColor}\" TintOpacity=\"0.3\" FallbackColor=\"{ThemeResource SystemChromeLowColor}\" />",
  "controlStyles[14].styles[1]": "CornerRadius=0",
  "controlStyles[14].styles[2]": "Margin=-2,0,-10,0",
  "controlStyles[15].target": "Taskbar.TaskListButtonPanel@CommonStates > Border#BackgroundElement",
  "controlStyles[15].styles[0]": "CornerRadius=5",
  "controlStyles[16].target": "taskbar:TaskListLabeledButtonPanel@RunningIndicatorStates > Border",
  "controlStyles[16].styles[0]": "CornerRadius=5",
  "controlStyles[17].target": "Taskbar.TaskListLabeledButtonPanel@CommonStates > Rectangle#RunningIndicator",
  "controlStyles[17].styles[0]": "Width=4",
  "controlStyles[17].styles[1]": "Height=4",
  "controlStyles[17].styles[2]": "RadiusX=10",
  "controlStyles[17].styles[3]": "RadiusY=10",
  "controlStyles[17].styles[4]": "Margin=0,-2,0,-2",
  "controlStyles[16].styles[1]": "Height=35"
}
```
⚬ Notification
```
{
  "controlStyles[0].target": "ScrollViewer#CalendarControlScrollViewer",
  "controlStyles[0].styles[0]": "BorderBrush:=<RevealBorderBrush Color=\"Transparent\" TargetTheme=\"1\" Opacity=\"0.8\"/>",
  "controlStyles[0].styles[1]": "Background:=<RevealBorderBrush Color=\"Transparent\" TargetTheme=\"1\" Opacity=\"0.3\"/>\t",
  "controlStyles[1].target": "Border#CalendarHeaderMinimizedOverlay",
  "controlStyles[1].styles[0]": "BorderBrush:=<RevealBorderBrush Color=\"Transparent\" TargetTheme=\"1\" Opacity=\"0.8\"/>",
  "controlStyles[1].styles[1]": "Background:=<RevealBorderBrush Color=\"Transparent\" TargetTheme=\"1\" Opacity=\"0.3\"/>\t",
  "controlStyles[2].target": "ActionCenter.FocusSessionControl",
  "controlStyles[2].styles[0]": "Height=0",
  "controlStyles[3].target": "Windows.UI.Xaml.Controls.TextBlock",
  "controlStyles[3].styles[0]": "Foreground:=#ffffff",
  "controlStyles[4].target": "Button#ExpandCollapseButton > ContentPresenter",
  "controlStyles[4].styles[1]": "Background:=<RevealBorderBrush Color=\"Transparent\" TargetTheme=\"1\" Opacity=\"0.3\"/>\t",
  "controlStyles[4].styles[0]": "BorderBrush:=<RevealBorderBrush Color=\"Transparent\" TargetTheme=\"1\" Opacity=\"1\"/>",
  "controlStyles[5].target": "Grid",
  "controlStyles[5].styles[0]": "RequestedTheme=2",
  "controlStyles[6].target": "ActionCenter.FlexibleItemView",
  "controlStyles[6].styles[0]": "CornerRadius=15",
  "controlStyles[7].target": "Windows.UI.Xaml.Controls.Primitives.ToggleButton#DoNotDisturbButton > Grid > ContentPresenter",
  "controlStyles[7].styles[0]": "Visibility=Collapsed"
}
```

## VI. Wrapping things up

### After installing and configuring apps and software:
- Reboot
- Start Menu:
	- `C:\Users\[NAME]\AppData\Roaming\Microsoft\Windows\Start Menu\Programs`
	- `C:\ProgramData\Microsoft\Windows\Start Menu\Programs`
	- right click on the app to Pin to Start
- Taskbar:
	- Pin to taskbar
	- System tray
- `Win + R`:
	- temp
	- %temp%
	- prefetch
	- `C:\Windows\SoftwareDistribution\Download`
	- cleanmgr
- Wintoys → Health:
	- Cleanup
	- Repair → check DISM and SFC → Scan

![[June 2025] Desktop](🀦/[June-2025]-Desktop.png)

**‧₊˚♪ PC is good to go 𝄞₊˚⊹**

### Afterthought:
- Originally, this guide was writen on Google Drive because it was a side project. As it snowballed into a full-fledged guide, maintaining and reviewing it became increasingly challenging. I was hesitant about migrating to GitHub since not everyone's a programmer but I had to take the plunge for the sake of maintenance and legibility.
- `Win + R → msinfo32 → System Summary → Components` to check what adapters your PC is using.

- **Windows 11**:
	> Why do I have to go through system modification?

	The truth of the matter is that *Windows 11 sucks*. It's filled with bloatware, unnecessary services running in the background, too much telemetry, and now AI nonsense no one asks for. **Microsoft keeps shooting itself in the foot**, so that's why.

	> Why do I have to disable so many unnecessary services?

	Well, even though disabling them has a negligible impact performance and battery life, you disable unnecessary services. DUH! After all not everyone has a printer at home (Print Spooler), use BitLocker (BitLocker Drive Encryption Service), or search files via Windows Search (Windows Search).

	> Why don't I just buy a Windows 11 product key?

	After all it's illegal and immoral to crack Windows 11 activation, but who cares lol. Micro$oft mainly operates on a *B2B model*, so Windows as an OS is neglected. Not only do you have to pay to use the service but also have your data harvested from using the service itself and have ads being shoved down your throat. It's utterly ridiculous.

	> Why do I have to navigate around menus like Run and Control Panel?

	Because that's where I get real work done. Just bear with the dark mode inconsistency. As said before, *Microsoft primarily caters to businesses*, and businesses being themselves, old interfaces stuck around.

	> Why some core applications of Windows 11 are omitted, such as Microsoft Photos?

	Here's the naked truth: they suck. *Microsoft Photos rely on WebView2 from Microsoft Edge*, so removing it means rendering that useless. Why do I need to rely on the web to view images locally on my PC? Also, Windows Media Player lacks codec support for obscure or specialized video and audio ones.

	> To download Microsoft Office, you have to to go through [Microsoft 365](https://microsoft.com/microsoft-365/microsoft-office "Microsoft"), which isn't free and is basically Microsoft Office bundled with OneDrive, Microsoft Teams, and other Microsoft productivity software.

	Somehow, I found the link to straight up download Microsoft 365 for free. Just don't ask me how, when, or that the link didn't work had Microsoft found out.

  	> Why Microsoft Office? It isn't free and there are better alternatives like LibreOffice and OpenOffice.

	I'm aware of such alternatives but I still prefer it because of Fluent design.

- [Linux](https://github.com/nhantrichuyenanh/linux-distro-ofb "nhantrichuyenanh")?
	> Why don't I switch to Linux already?

	I could have gone with Linux distros like Linux Mint or Arch Linux, but I still stick with Windows since I spent a decade using it. I've memorized all the hotkeys (**⊞**), directory structure (**C:**), system applications (**File Explorer**), OS security (**UAC**), and GUI (<sup>Windows shell</sup>**Metro / Fluent**) for it. Moving to Linux meant that I would have to relearn everything from hotkeys (**❖**), directory structure (**/**), system applications (**Nemo / Dolphin / Nautilus / ...**), OS security (**sudo**) and GUI (<sup>Linux DEs</sup>**Cinnamon / KDE Plasma / GNOME / ...**). Not only that but I would have to also have to learn how to use the terminal emulator and commands for it too. It's too much of an upfront investment.

	> Linux is indubitably better than Windows in every front.

	Yes, I can't agree more. It gives power to the user, so you must be a power user (no pun intended lol). You're responsible dealing with issues should they occur, often on your own. But the upside is that it's extremely customizable, blazing fast, boots up fast, takes up little memory and RAM, and none of the aforementioned downsides of Windows. Like Felix Kjellberg said, Linux is built modular. You can swap your GUI entirely, unlike Windows 10/11 which you're stuck with Metro/Fluent UI.

	> Why do I use Windows 11 but not [Windows 11 Enterprise LTSC](https://microsoft.com/en-us/evalcenter/download-windows-11-enterprise "Microsoft")/[Enterprise IoT LSTC](https://microsoft.com/en-us/evalcenter/download-windows-11-iot-enterprise-ltsc-eval "Microsoft")?

	Simple. Because the latter doesn't release feature updates. I actually have used it before and it's indeed much faster, no bloatware and AI nonsense but still have telemetry and some unnecessary services running in the background.

	> What about other Windows 11 ISO?

	No, don't even consider them. I high discourage installing custom ISOs because of security. What if they slip malware, spyware, or keyloggers into them? Installing these sketchy Windows 11 ISOs means there's a high degree of trust involved.

- Main & Additional Browser:
	> [Chromium-based](https://wikipedia.org/wiki/Chromium_(web_browser)#Differences_from_Google_Chrome "Wikipedia") includes Chrome and other browsers based on Chromium while [Firefox fork](https://wikipedia.org/wiki/Category:Web_browsers_based_on_Firefox "Wikipedia") includes Firefox and other browsers based on Firefox

	 - Generally speaking, Chromium-based browsers are more **privacy invasive** (except for some notable ones like Brave) but **well established** since almost all websites and extentions are built and optimized for them. Firefox fork ones, meanwhile, are more **privacy and security-centric**, and some even offer **speed and customizablity**.
	 - As for me personally, just don't use Chrome (or even Firefox for that matter), opt for something else. Playing devil's advocate, Chrome is really good because it has to be that way (we use Google services via the web, not desktop apps, so it makes sense it's in Google's interest to make Chrome good). The same thing can't be said for Firefox, as it's only saving grace is not being Chromium-based.
	 - Edge, despite being heavily bloated, privacy invasive, and having AI nonsense, is extremely good. It's **well optimized** for performance and battery life, packed with lots of **nice and useful features** (e.g. vertical tabs, split screen, video enhancement), and supports **Fluent design**. You can fix Edge through third party tools or just use it straight out of the box if you don't mind.
	 - Ultimately, I highly recommend doing your homework and downloading the browsers that you don't mind the downsides. Each has its strong suit, the factor that you should care about. If you just want to surf the web and isn't bothered by Big Tech, stick with _Chrome_ or _Edge_. Maybe you want to jump on the bandwagon, then give _Comet_ or _Deta Surf_ a shot. But in the user experience and interface department, _Zen Browser_ stands out. You get the idea.

- File Sharing Software:
	> Why don't I just use cloud storage services like Google Drive? Or use Phone Link instead?

 	- Because uploading and downloading files on cloud storage services exponentially take up time, and most of the time I simply need to quicky send over a photo. And besides, I have no intention of turning on Bluetooth every time to use Phone Link.
  	- I've tried LocalSend before, and currently using Blip because of Fluent design.

- PDF Software:
	> [List of PDF software on Windows](https://wikipedia.org/wiki/List_of_PDF_software#Microsoft_Windows)

	 - Freemium ones have the bells and whistles like modern UI, smooth scrolling, and AI assistant.
	 - Meanwhile, completely free ones have a certain rustic charm and embrace minimalism.
	 - FYI, I'm currently using PDF24 and have used Foxit PDF Reader, Wondershare PDFelement, and PDFgear before. The last one was pleasantly nice but it was slow when launching it after opening a PDF file and lacked support for thumbnail previews.

> [!NOTE]
> Even though this guide is for my personal use for Windows reinstallation, hopefully you guys find it informative and beneficial. Enjoy using Windows! ヾ(•ω•`)o
