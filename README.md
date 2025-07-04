# Windows 11 Order of Business:
![Illustration](🀦/MS_EMOJI_310_v002_4k_1084.jpg "Microsoft Design")
> [!IMPORTANT]
> This guide assumes you can navigate Windows using menu interfaces and know what adapters your PC is using. Check [here](#afterthought) for Q&A.

| Section | Subsection | Description |
|--------|------------|-------------|
| [I. Preparations](#i-preparations) | | Initial preparations before system changes. |
| [II. System modifications](#ii-system-modifications) | [1. System modification](#1-system-modification) | Tweak system settings. |
|  | [2. Disable unnecessary services](#2-disable-unnecessary-services) | Self-explanatory. |
|  | [3. Disable stealing bandwidth](#3-disable-stealing-bandwidth) | Prevent Microsoft from consuming bandwidth. |
|  | [4. Enable Clipboard History](#4-enable-clipboard-history) | Enable `Win + .` |
|  | [5. Disable bufferless tracking](#5-disable-bufferless-tracking) | Disable diagnostic tracking of NBL ownership in the NDIS layer. |
|  | [6. Registry Hacks](#6-registry-hacks) | Apply useful registry tweaks. |
|  | [7. Turn off useless Windows Features](#7-turn-off-useless-windows-features) | Self-explanatory. |
| [III. Setting things up](#iii-setting-things-up) | [1. Mouse Cursor and Font](#1-mouse-cursor-and-font) | Self-explanatory. |
|  | [2. AccentColorizer](#2-accentcolorizer) | Colorize Windows with accent color. |
|  | [3. File Explorer](#3-file-explorer) | File Explorer configurations. |
|  | [4. Settings](#4-settings) | Activate Windows and `Win + I` configurations. |
|  | [5. Control Panel](#5-control-panel) | System Properties, Region, Power Options, Internet Properties, Sound, and Network Connections configurations. |
|  | [6. Device Manager](#6-device-manager) | Disable unused devices and drivers. |
| [IV. Installing software](#iv-installing-software) | | Install applications. |
| [V. Configuring software](#v-configuring-software) | | Customize applications. |
| [VI. Wrapping things up](#vi-wrapping-things-up) | [After installing and configuring apps and software](#after-installing-and-configuring-apps-and-software) | Cleanup. |
|  | [Afterthought](#afterthought) | Q&A |


---

## I. Preparations

After Windows 11 is installed:
- boot into BIOS to enable Fastboot if haven't. I thoroughly recommend exploring other settings to optimize BIOS, provided that you know what you're doing or seek guidance from AI if you're uncertain;
- immediately `Win + I → Windows Update → Check for updates`. You might have to do this once or twice. Also, check `System → Storage → Remove Temporary Files` while you're at it;
- update BIOS by visiting your PC manufacturer's website and drivers via Windows Update, your PC manufacturer's website, or third-party tools like [Snappy Driver Installer](https://sdi-tool.org/download/ "Glenn Delahoy");
- (OPTIONAL) join Windows Insider Program. You get early access to new features, like **text extractor** and **color picker** in Snipping Tool, basic **text formatting** options in Notepad, and **battery percentage** in Taskbar as of writing this in June 2025. Don't join if your Windows 11 is Enterprise LTSC/Enterprise IoT LSTC, or you want maximum stability and don't care about feature updates. [🔍︎](https://youtu.be/YQFx6C6SL08 "ThioJoe")

---

## II. System modifications

`Win + R → UserAccountControlSettings` → drag the slider all the way down → OK

### 1. System modification:

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

### 2. Disable unnecessary services:
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

### 3. Disable stealing bandwidth:
- `Win + R → gpedit.msc → Computer Configuration → Administrative Templates → Network → QoS Packet Scheduler → Limit reservable bandwidth → Enable → Bandwidth limit (%): 0`
- `Win + R → regedit → Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft → New > Key → Psched → New > DWORD (32-bit) Value → NonBestEffortLimit`

### 4. Enable Clipboard History:
- `Win + R → regedit → Computer\HKEY_CURRENT_USER\Software\Microsoft\Clipboard → EnableClipboardHistory → 1`
- `Win + R → gpedit.msc → Computer Configuration → Administrative Templates → System → OS Policies → Allow Clipboard History → Enable`

### 5. Disable bufferless tracking:
`Win + R → regedit → HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NDIS\Parameters → TrackNblOwner → Value data: 0`

### 6. [Registry Hacks](https://vinstartheme.com/unlock-windows-hidden-features "VIN STAR")

### 7. Turn off useless Windows Features:
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
  - [Mica Explorer](https://github.com/Maplespe/ExplorerBlurMica "Maplespe")
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

  - **Network Connections**: `Win + R → ncpa.cpl` → double click / right click on the network connection you're using (most likely Ethernet or Wi-Fi) → Properties
     - Network connection Properties: uncheck
     	- Client for Microsoft Networks
     	- File and Printer Sharing for Microsoft Networks
     	- Microsoft LLDP Protocol Driver
     	- Internet Protocol Version 6 (TCP/IPv6) `(uncheck if you don't use` [IPv6](https://test-ipv6.com)`)`
     	- Link-Layer Topology Discovery Responder
     	- Link-Layer Topology Discovery Mapper I/O Driver
    - Internet Protocol Version 4 (TCP/IPv4) → Properties → Use the following DNS server addresses: Preferred DNS server is **1.1.1.1** and Alternate DNS server is **1.0.0.1** → Close
    - Network adapter Properties: double click / right click on the network connection you're using → Properties → Configure... 
      - Power Management → uncheck Allow the computer to turn off this device to save power
      - Advanced → screenshot the window and ask AI which ones to fine-tune for network performance → OK
    - `Win + R → ncpa.cpl` → right click on Bluetooth Network Connection → Properties → uncheck:
      	- Client for Microsoft Networks `(if you don't intent on sharing files or printers)`
      	- File and Printer Sharing `(if you don't intent on sharing files or printers)`
      	- Microsoft Network Adapter Multiplexor Protocol
      	- Microsoft LLDP Protocol Driver
      	- Link-Layer Topology Discovery Responder
      	- Link-Layer Topology Discovery Mapper I/O Driver
      	- Internet Protocol Version 6 (TCP/IPv6) `(if your Bluetooth PAN doesn't need IPv6, run the command below in Admin PowerShell to determine if it is enabled or not)`
```
Get-NetAdapterBinding -Name "Bluetooth Network Connection" | Where-Object DisplayName -Match "Internet Protocol"
```

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
- Main & Additional Browser: [🔍︎](#afterthought "Afterthought")
	- Chromium-based: [Brave](https://brave.com/download "Brendan Eich and Brian Bondy") / [Deta Surf](https://deta.surf "Deta") / [Vivaldi](https://vivaldi.com/download "Vivaldi Technologies") / ...
	- Firefox fork: [Floorp](https:/floorp.app/en-US/download "Floorp Projects") / [Librewolf](https://librewolf.net/installation/windows) / [Zen Browser](https://zen-browser.app/download "Zen Browser Team") / ...

A
- [AB Download Manager](https://abdownloadmanager.com)
- [Audacity](https://audacityteam.org/download/windows)

B
- [BCUninstaller](https://sourceforge.net/projects/bulk-crap-uninstaller)

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
- [PDFgear](https://pdfgear.com/pdfgear-for-windows)
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
- [StartAllBack](https://startallback.com)

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
	- `chrome://flags` (Chromium-based) / `about:config` (Firefox fork) [🔍︎](🗀/BrowserModification.md "Browser Modification")
	- [Bypass Paywalls Clean](https://gitflic.ru/project/magnolia1234/bpc_uploads "magnolia1234")

![[June 2025] Floorp Homepage](🀦/[June-2025]-Floorp-Homepage.png)

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
	- Windows 11 Styler
| Column 1 | Column 2 | Column 3 |
|----------|----------|----------|
| Value 1  | Value 2  | Value 3  |

	- Windows 11 Start Menu Styler
```
a
```
‎
	- Windows 11 Taskbar Styler
```
a
```
‎
‎
	- Windows 11 Notification Styler
```
b
```

---

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
- `Win + R → cmd → Ctrl + Shift + Enter`: to check if ieframe.dll is corrupted because it’s a core component of Internet Explorer `(even though it is deprecated, some legacy applications and internal tools might still depend on it)`
```
sfc /scanfile=C:\Windows\System32\ieframe.dll
sfc /verifyfile=C:\Windows\System32\ieframe.dll
```

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

	After all it's illegal and immoral to crack Windows 11 activation, but who cares lol. Micro$oft mainly operates on a *B2B model*, so Windows as an OS is neglected. Not only do you have to pay to use the service but have your data harvested from using the service itself while having ads being shoved down your throat. It's utterly ridiculous.

	> Why do I have to navigate around menus like Run and Control Panel?

	Because that's where I get real work done. Just bear with the dark mode inconsistency. As said before, *Microsoft primarily caters to businesses*, and businesses being themselves, old interfaces stuck around.

	> Why some core applications of Windows 11 are omitted, such as Microsoft Photos?

	Here's the naked truth: they suck. *Microsoft Photos rely on WebView2 from Microsoft Edge*, so removing it means rendering that useless. Why do I need to rely on the web to view images locally on my PC? Also, Windows Media Player lacks codec support for obscure or specialized video and audio ones.

	> To download Microsoft Office, you have to to go through [Microsoft 365](https://microsoft.com/microsoft-365/microsoft-office "Microsoft"), which isn't free and is basically Microsoft Office bundled with OneDrive, Microsoft Teams, and other Microsoft productivity software.

	Somehow, I found the link to straight up download Microsoft 365 for free. Just don't ask me how, when, or that the link didn't work had Microsoft found out.

- [Linux](https://github.com/nhantrichuyenanh/linux-distro-ofb "nhantrichuyenanh")?
	> Why don't I switch to Linux already?

	I could have gone with Linux distros like Linux Mint or Arch Linux, but I still stick with Windows since I spent a decade using it. I've memorized all the hotkeys (**⊞**), directory structure (**C:**), system applications (**File Explorer**), OS security (**UAC**), and GUI (<sup>Windows shell</sup>**Metro / Fluent**) for it. Moving to Linux meant that I would have to relearn everything from hotkeys (**❖**), directory structure (**/**), system applications (**Nemo / Dolphin / Nautilus / ...**), OS security (**sudo**) and GUI (<sup>Linux DEs</sup>**Cinnamon / KDE Plasma / GNOME / ...**). Not only that but I would have to also have to learn how to use the terminal emulator and commands for it too. It's too much of an upfront investment.

	> Linux is indubitably better than Windows in every front.

	Yes, I can't agree more. It gives power to the user, so you must be a power user (no pun intended lol). You're responsible dealing with issues should they occur, often on your own. But the upside is that it's extremely customizable, blazing fast, boots up fast, takes up little memory and RAM, and none of the aforementioned downsides of Windows. Like Felix Kjellberg said, Linux is built modular. You can swap your GUI entirely, unlike Windows 10/11 which you're stuck with Metro/Fluent UI.

	> Why do I use Windows 11 but not [Windows 11 Enterprise LTSC](https://microsoft.com/en-us/evalcenter/download-windows-11-enterprise "Microsoft")/[Enterprise IoT LSTC](https://microsoft.com/en-us/evalcenter/download-windows-11-iot-enterprise-ltsc-eval "Microsoft")?

	Simple. Because the latter doesn't release feature updates. I actually have used it before and it's indeed much faster, no bloatware and AI nonsense but still have telemetry and some unnecessary services running in the background.

	> What about other Windows 11 ISO?

	No, don't even consider them. I high discourage installing custom ISOs because of security. What if they slip malware, spyware, or keyloggers into them? Installing these sketchy Windows 11 ISOs means there's a high degree of trust involved.

- [Main & Additional Browser]: Please do your research and download your desired browser(s) at your own discretion.
	> [Chromium-based](https://wikipedia.org/wiki/Chromium_(web_browser)#Differences_from_Google_Chrome "Wikipedia") includes Chrome and other browsers based on Chromium while [Firefox fork](https://wikipedia.org/wiki/Category:Web_browsers_based_on_Firefox "Wikipedia") includes Firefox and other browsers based on Firefox

	 - Generally, Chromium-based browsers are more **privacy invasive** (except for some notable ones like Brave) but **well established** since almost all websites and extentions are built and optimized for them. Firefox fork ones, meanwhile, are more **privacy and security-centric**, and some even offer **speed and customizablity**.
	 - As for me personally, just don't use Chrome (or even Firefox for that matter), opt for something else.
	 - Edge, despite being heavily bloated, privacy invasive, and having AI nonsense, is extremely good. It's **well optimized** for performance and battery life, packed with lots of **nice and useful features** (e.g. vertical tabs, split screen, video enhancement), and supports **Fluent design**. You can fix Edge through third party tools or just use it straight out of the box if you don't mind.

> [!NOTE]
> Even though this guide is for my personal use for Windows reinstallation, hopefully you guys find it informative and beneficial. Enjoy using Windows! ヾ(•ω•`)o
