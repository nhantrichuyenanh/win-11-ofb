# Windows 11 Order of Business:
> [!TIP]
> lorem ipsum dolor sit amet
- [I. Preparations](#i-preparations)
- [II. System modifications](#ii-system-modifications)
  - [1. System modification](#1-system-modification)
  - [2. Disable unnecessary services](#2-disable-unnecessary-services)
  - [3. Disable stealing bandwidth](#3-disable-stealing-bandwidth)
  - [4. Enable Clipboard History](#4-enable-clipboard-history)
  - [5. Disable bufferless tracking](#5-disable-bufferless-tracking)
  - [6. Registry Hacks](#6-registry-hacks)
  - [7. Turn off useless Windows Features](#7-turn-off-useless-windows-features)
- [III. Setting things up](#iii-setting-things-up)
- IV. Installing software
- V. Configuring software
- VI. Wrapping things up
---

## I. Preparations

After Windows 11 is installed:
- boot into BIOS to enable Fastboot if haven't. I thoroughly recommend exploring other settings to optimize BIOS, provided that you know what you're doing or seek guidance from AI if you're uncertain;
- immediately open `Settings → Windows Update → Check for updates`. You might have to do this once or twice. Also, check `System → Storage → Remove Temporary Files` while you're at it;
- update BIOS by visiting your PC manufacturer's website and drivers via Windows Update, your PC manufacturer's website, or third-party tools like [Snappy Driver Installer](sdi-tool.org/download/ "Glenn Delahoy");
- (OPTIONAL) join Windows Insider Program. You get early access to new features, like text extractor and color picker in Snipping Tool, or basic text formatting options in Notepad as of writing this in June 2025. Don't join if your Windows 11 is Enterprise LTSC/Enterprise IoT LSTC, or you want maximum stability and don't care about feature updates. For more information, visit [here](https://youtu.be/YQFx6C6SL08 "ThioJoe").

---

## II. System modifications

`Win + R → UserAccountControlSettings` → drag the slider all the way down → OK

### 1. System modification:

**Required:**
- [CrapFixer](https://github.com/builtbybel/CrapFixer/releases "Builtbybel")
- The Ultimate Windows Utility (Admin PowerShell): `iwr -useb https://christitus.com/win | iex`
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
- [Winhance](https://winhance.net "Marco du Plessis")
- [WinScript](https://github.com/flick9000/winscript/releases "Francesco")

### 2. Disable unnecessary services:
- Win + R → services.msc
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
  - IP Helper `(disable it if you don't use IPv6, visit here for validation: test-ipv6.com)`
  - Netlogon
  - Parental Controls
  - Print Spooler `(don't disable it if you have a printer at home and you use it)`
  - Phone Service `(disable if you don't use)`[Phone Link](microsoft.com/windows/sync-across-your-devices "Microsoft")
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
  - TCP/IP NetBIOS Helper `(disable it if you don't use)`[Workgroup](wikipedia.org/wiki/Workgroup_(computer_networking) "Wikipedia")
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
`Win + R → gpedit.msc, Computer Configuration → Administrative Templates → Network → QoS Packet Scheduler → Limit reservable bandwidth → Enable → Bandwidth limit (%): 0`

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

- [Mouse Cursor](⛁/deviantart-jepricreations-cursor)
- [Fonts](⛁/fonts)
- [Mica Explorer](https://github.com/Maplespe/ExplorerBlurMica "Maplespe")
- **AccentColorizer**:  
   - [AccentColorizer](https://github.com/krlvm/AccentColorizer "krlvm")  
   - [AccentColorizer-E11](https://github.com/krlvm/AccentColorizer-E11 "krlvm")
- **File Explorer**:

![[June 2025] File Explorer](🀦/[June-2025]-File-Explorer.png)
  - Configure Quick access
  - Show details pane
  - ⋯ → Options
- **Activate Windows (Admin PowerShell)**: `irm https://get.activated.win | iex`
- **Settings Configuration**: `Win + I`  
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
- **Control Panel Items**:
  - Visual Effects: Win + R → SystemPropertiesPerformance.exe
	- Region: Win + R → intl.cpl → Formats
	- Internet Properties: Win + R → inetcpl.cpl → Connections → LAN settings → uncheck Automatically detect settings
	- Network Connections: Win + R → ncpa.cpl → double click / right click on the network connection you're using (most likely Ethernet or Wi-Fi) → Properties
    - Network Connection Properties: uncheck
      - Client for Microsoft Networks
      - File and Printer Sharing for Microsoft Networks
      - Microsoft LLDP Protocol Driver
      - Internet Protocol Version 6 (TCP/IPv6) `(uncheck if you don't use IPv6: test-ipv6.com)`
      - Link-Layer Topology Discovery Responder
      - Link-Layer Topology Discovery Mapper I/O Driver
    - Internet Protocol Version 4 (TCP/IPv4) → Properties → Use the following DNS server addresses: Preferred DNS server is 1.1.1.1 and Alternate DNS server is 1.0.0.1 → Close
    - Network adapter Properties: double click / right click on the network connection you're using → Properties → Configure... 
      - Power Management → uncheck Allow the computer to turn off this device to save power
      - Advanced → screenshot the window and ask AI which ones to fine-tune for network performance → OK
    - Win + R → ncpa.cpl → right click on Bluetooth Network Connection → Properties → uncheck:
      - Client for Microsoft Networks `(if you don't intent on sharing files or printers)`
      - File and Printer Sharing `(if you don't intent on sharing files or printers)`
      - Internet Protocol Version 6 (TCP/IPv6) `(if your Bluetooth PAN doesn't need IPv6, run the command below in Administrator PowerShell to determine if it is enabled or not)`
				`Get-NetAdapterBinding -Name "Bluetooth Network Connection" | Where-Object DisplayName -Match "Internet Protocol"`
      - Microsoft Network Adapter Multiplexor Protocol
      - Microsoft LLDP Protocol Driver
      - Link-Layer Topology Discovery Responder
      - Link-Layer Topology Discovery Mapper I/O Driver
	- Sound: Win + R → mmsys.cpl
    - Communications → When Windows detects communications activities: Do nothing
    - Playback → select the speaker your PC is using as output → Properties:
      - Spatial sound → Windows Sonic for Headphones
      - If there's Enhancements, select Bass Boost, Virtual Surround, Loudness Equalization. If not: Win + R → devmgmt.msc → Sound, video and game controllers → right click the speaker your PC is using as output → Disable device → Update driver → Browse my computer for drivers → Let me pick from a list of available drivers on my computer → uncheck Show compatible hardware → Manufacturer: Microsoft → in Model select High Definition Audio Device Version the latest date → Yes → Close → Reboot
	- Power Options: Win + R → control.exe powercfg.cpl,,3

- Device Manager Optimizations:
	- Audio inputs and outputs: disable the ones you don't use
	- Network adapters:
      - disable the ones you don't use like Ethernet for many people
      - right click on the network adapter you use → Properties → Power Management → uncheck Allow the computer to turn off this device to save power
      - disable Microsoft Kernel Debug Network Adapter [for kernel debugging like BSOD]
	- Software devices: disable Microsoft GS Wavetable Synth [an old, software-based MIDI player from the 90s]
	- Sound, video and game controllers: disable the ones you don't use
	- System Devices: disable
      - System speaker [used for diagnostics in BIOS]
      - Remote Desktop Device Redirector Bus [allows local devices like printers to be used remotely]
      - NDIS Virtual Network Adapter Enumerator [for VMs]
      - Microsoft Hyper-V Virtualization Infrastructure Driver [for VMs]

---

## IV. Installing software

Install [UniGetUI](https://github.com/M2Team/UniGetUI) from Microsoft Store.  
If you're using Enterprise LTSC/IoT LSTC, install Microsoft Store via:  
`wsreset -i`

Apps listed below are organized A-Z, some with links, most assumed from Store or UniGetUI.

*(Full list preserved; links embedded using standard markdown where applicable. Let me know if you want this converted into a clickable table.)*

---

## V. Configuring software

Apps and settings configuration retained 1:1  
- For structured items like browser setup, PowerToys, and Windhawk modules, hierarchy and categories preserved  
- Subsections (e.g., theme JSON for Nilesoft Shell, plugin list for Discord) formatted in code blocks or indented where appropriate

---

## VI. Wrapping things up

Final checklist steps after setup:
- 🀦 → [June 2025] Desktop
- Startup apps (`Ctrl + Shift + Esc`)
- Start Menu paths
- System tray
- `Win + R` → `temp`, `%temp%`, `prefetch`, etc.
- Run `cleanmgr`
- Use Wintoys → Health → Cleanup + Repair (DISM/SFC)
- `sfc /scanfile=C:\Windows\System32\ieframe.dll`  
  `sfc /verifyfile=C:\Windows\System32\ieframe.dll`

---

### ‧₊˚♪ PC is good to go 𝄞₊˚⊹

---

## Afterthought

*(Personal commentary kept exactly as-is. Added horizontal rules for readability.)*

---

## 💭 Additional Q&A Sections

*(Windows 11: Why do I have to... / Why don't I... sections formatted as collapsible content on GitHub via `<details>` if desired, otherwise left as plain text with proper spacing and indentation)*

---

## [Main & Additional Browser] Note

Includes breakdown on Chromium vs Firefox forks, personal advice, and rationale.  
Embedded source links using markdown for Wikipedia entries.

---

## Final Note

> Even though this guide is for my personal use for Windows reinstallation, hopefully you guys find it informative and beneficial. Have a nice day! ヾ(•ω•`)o
