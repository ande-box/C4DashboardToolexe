# 🎛️ C4DashboardTool (Beta Edition)

A standalone Windows application for monitoring and controlling your **Control4** smart home system via the Director API. Just download, configure, and run.

> **🔐 BETA NOTICE:** This application is currently in an open Beta phase. It is hardcoded to run freely until **January 1, 2027**. After this date, a valid license key will be required to use the software.

> **🆕 New in v260915:** On-Demand License Check — verify your license status at any time from Setup Mode (**🛡️ Check License**), with live `.env` re-read so new keys activate **without restarting** the application.

---

## 📦 What's Included

| File | Purpose |
|------|---------|
| `C4DashboardTool.exe` | The main application (compiled Python executable with embedded UI and public key) |
| `.env` | Your credentials and settings (must be configured) |
| `dashboard_config.json` | Your dashboard layout and widgets (auto-managed) |

> **Note:** The `public_key.pem` file is now **embedded inside the .exe** and is no longer included as a separate file. The `templates/dashboard.html` file is also embedded.

---

## 🚀 Quick Start

### Step 1: Download All Files
Ensure all three files (`C4DashboardTool.exe`, `.env`, `dashboard_config.json`) are in the **same folder** on your computer.

### Step 2: Configure `.env`
Open the `.env` file with any text editor (Notepad, VS Code, etc.) and update the following:

```env
C4_USERNAME="your_control4_email@example.com"
C4_PASSWORD="your_control4_password"
C4_HOST="192.168.1.XX"
C4_GUI_PORT=65003
C4_AUTO_OPEN_BROWSER=true
C4_POLLING_INTERVAL_MS=1000
NTP_ADDRESS="89.109.251.21"
LICENSE_KEY=""
```

| Variable | Description |
|----------|-------------|
| `C4_USERNAME` | Your Control4 account email |
| `C4_PASSWORD` | Your Control4 account password |
| `C4_HOST` | IP address of your Control4 controller |
| `C4_GUI_PORT` | Port for the web dashboard (default: 65003) |
| `C4_AUTO_OPEN_BROWSER` | `true` = opens browser automatically on startup |
| `C4_POLLING_INTERVAL_MS` | How often to refresh widget data (in milliseconds) |
| `NTP_ADDRESS` | NTP server used for secure time verification (optional) |
| `LICENSE_KEY` | Currently bypassed by Beta Dateguard. Paste your license key here after Jan 1, 2027. Use the **🛡️ Check License** button (Setup Mode) to verify it on demand — no restart needed. |

### Step 3: Run the Application
Double-click `C4DashboardTool.exe`.

A console window will appear showing detailed licensing and connection logs, and your default browser will open the dashboard at `http://127.0.0.1:65003` (or your configured port).

---

## ️ Licensing & Beta Status

### Current Beta Status
The application is currently in an open Beta phase. A hardcoded Dateguard allows the app to run freely without a key until **January 1, 2027**.

The bottom-right corner of the dashboard will display the current status:
`v260915 | License valid till Jan 01, 2027`

### Detailed License Logging
The application now provides detailed console logging for both the DateGuard and License verification steps, including:
- Days remaining until the Beta period expires
- Whether the license key is empty, invalid, expired, or valid
- Hardware match results (X/3 IDs matched)
- Specific error reasons if verification fails

### Requesting a License Key
In **Setup Mode**, click the **🔑 Request License** button in the header to open a modal displaying your Hardware IDs (OS GUID, CPU ID, MAC Address). Click **📋 Copy All IDs** to copy them to your clipboard, then send them to the developer to receive your license key.

### 🛡️ On-Demand License Check (New in v260915)
In **Setup Mode**, click the **🛡️ Check License** button to run a live license validation at any time — even during the Beta period. The result popup shows:
- ✅ **VALID** / ❌ **INVALID** status with the exact reason (Beta period active, license verified, key empty/expired/invalid, hardware mismatch X/3, etc.)
- The **"Valid till"** date (Beta end date or license expiry date)
- Your **Hardware IDs** (OS GUID, CPU ID, MAC Address)

The `.env` file is **re-read on every check**, so after pasting a new `LICENSE_KEY` you can verify and activate it immediately — **without restarting the application**.

The **"Access Denied"** screen (shown when licensing fails) also includes a **🔄 Re-check License** button: once a valid key is pasted into `.env`, clicking it re-validates and automatically reloads the dashboard.

### Post-Beta Activation
After January 1, 2027, the application will enforce its secure licensing system and will require a valid license key to run.
* If you need a license key after the Beta period, please contact the developer.
* After pasting the key into `LICENSE_KEY` in your `.env`, click **🛡️ Check License** (or **🔄 Re-check License** on the Access Denied screen) — the new key is verified and activated instantly, with no restart required.

---

## 🛠️ Using the Dashboard

### First Time Setup
1. Click **"Enter Setup Mode"** in the top-right corner.
2. Click **"️ Add Widget"** to create your first widget.
3. Follow the wizard:
   - **Step 1:** Choose widget type: **Button**, **Textbox**, **Combo-Button**, **MACRO**, or **🔍 API Explorer**.
   - **Step 2:** Select your device(s) using the **Quick Search bar**.
   - **Step 3:** Configure commands using the **3-Tab Command Selector**:
     - **📱 From Device** - Commands derived from the selected device's capabilities
     - **📚 From Library** - Categorized predetermined commands with parameter hints
     - **✏️ Custom** - Freestyle command entry with JSON parameters
   - **Step 4:** Configure parameters, **Filter Patterns**, and **Dynamic Color Rules**. For MACROs, build your timeline.
   - **Step 5:** Set a label and assign to a room.
4. Click **"✅ Save & Close"**.

### ✨ Features & UI Improvements

**🛡️ On-Demand License Check (New in v260915)**
- **One-click verification:** the **🛡️ Check License** button in Setup Mode runs a full license check on demand.
- **Result popup:** ✅/❌ status, exact reason, "Valid till" date, and Hardware IDs.
- **No restart needed:** `.env` is re-read on every check, so newly pasted keys take effect immediately.
- **Access Denied recovery:** the **🔄 Re-check License** button on the denied screen re-validates and reloads automatically.

**🔍 API Explorer Widget**
A new widget type to monitor raw API data, device variables, and system info using GET requests.
- **Categorized Methods** - Browse methods by category: Information & Discovery, Variables & Device Info, Item Commands, and Relay State
- **Advanced Filtering** - Use Filter Patterns to extract specific data from JSON responses
- **Dedicated Test Button** - Test your API Explorer configuration before saving
- **Auto-Polling** - Like Textbox widgets, API Explorer widgets automatically refresh at the configured interval

**📚 3-Tab Command Selector**
A completely redesigned command selection interface with three distinct sources:
- **📱 From Device** - Commands automatically derived from the selected device's capabilities
- **📚 From Library** - Categorized predetermined commands (Lighting, Climate, Blinds, Audio, Scenes, Locks, Relays, Rooms, Fans) with detailed parameter descriptions and examples
- **✏️ Custom** - Freestyle command entry for any Control4 API command

** Enhanced Test Modal**
Replaced small toast notifications with a full-sized popup for test results.
- **Clear Status** - Shows ✅ success or ❌ failure with descriptive titles
- **Full Result Display** - Complete test output without truncation
- **📋 Copy Button** - Copy results to clipboard for debugging
- **✕ Close Button** - Dismiss the modal when done

**🔄 Unified Filter Patterns**
Advanced JSON filtering syntax across all monitoring widgets (Textbox, Combo, API Explorer):
- **Extract a value:** `"name"`
- **Add literal text:** `'Temp: ' & "TEMPERATURE"`
- **Multiple fields:** `"name", "song"` (comma-separated)
- **Get all matches:** `"name"|||` (finds nested duplicates)
- **Combine fields:** `"name" & "song"` or `("name" + "song")`

**📦 Expanded Command Library**
Integrated official commands and getters based on `pyControl4` documentation:
- **Lighting** - ON, OFF, SET_LEVEL, RAMP_TO_LEVEL, SET_COLOR_TARGET (XY and Temperature)
- **Climate/Thermostat** - SET_SETPOINT_HEAT/COOL (Celsius/Fahrenheit), SET_MODE_FAN/HVAC/HOLD, SET_PRESET
- **Blinds/Shades** - SET_LEVEL_TARGET (OPEN/CLOSED), STOP, TOGGLE, plus getters for Level, Battery, Opening/Closing state
- **Audio/Volume** - Volume up/down/mute/set, media play/pause/stop
- **Scenes** - Activate/Deactivate
- **Locks & Relays** - LOCK, UNLOCK, OPEN, CLOSE, TOGGLE, plus state getters
- **Rooms** - ROOM_OFF, SET_VOLUME_LEVEL, MUTE_ON/OFF/TOGGLE, SELECT_AUDIO/VIDEO_MEDIA/DEVICE, SEND_KEY
- **Fans** - SET_SPEED, DESIGNATE_PRESET
- **Security/Alarms** - PARTITION_ARM/DISARM, EXECUTE_EMERGENCY, KEY_PRESS, plus state getters

**🔑 One-Click License Request**
In Setup Mode, click the **🔑 Request License** button to instantly view and copy your Hardware IDs (OS GUID, CPU ID, MAC Address) to the clipboard.

**🎯 Global Command Preview**
A preview box at the top of Step 3 shows exactly which command will be saved, regardless of which tab (Device/Library/Custom) you're currently viewing.

**🎬 MACRO Widget (Scene Director)**
A powerful widget type for executing complex batch commands.
- **Parallel & Serial Execution:** Commands in the same row run concurrently; rows run sequentially.
- **Configurable Delays:** Add a delay (up to 60 seconds) before *any* row executes.
- **Visual Feedback:** The widget pulses with a smooth color animation while running.

**🎨 Dynamic Color Rules**
Automatically change a widget's **Left Border Accent and Background Tint** based on specific variable values (e.g., Green for "True", Red for "Error").

**🔗 Combo-Button (2-in-1 Widget)**
A hybrid widget that acts as a clickable button to send a command while simultaneously polling and displaying a live status variable.

**📱 Smart Mobile UI**
- **Smart Shutdown Button:** Hidden on mobile devices to prevent accidental server shutdowns.
- **Mobile Setup Restriction:** Setup controls are hidden on mobile to keep the interface clean.
- **Cleaner Pure Buttons:** Standard Buttons are rendered as clean, compact cards.

**🏠 Room Management & Reordering**
- Create rooms and filter views via tabs.
- Drag and drop widgets using the **⋮ handle** in Setup Mode.
- The dashboard uses a **Masonry Layout** to dynamically resize widgets without stretching rows.
- Long widget titles now automatically wrap to multiple lines.

**📊 Status Monitoring Divider**
A visual divider labeled "STATUS MONITORING" separates command configuration from status variable selection, making the setup process clearer.

---

## ⚠️ Important Notes

### 🔌 Check That Your Port Is Free Before Launching
The application binds to the port specified in `C4_GUI_PORT` (default: **65003**). If another application — or **another running instance of C4DashboardTool itself** — is already using that port, the dashboard will fail to start.

**Before launching**, open **PowerShell** (run as Administrator for full details) and verify the port is not occupied:

```powershell
Get-NetTCPConnection -LocalPort 65003 -ErrorAction SilentlyContinue | ForEach-Object {
    $proc = Get-Process -Id $_.OwningProcess -ErrorAction SilentlyContinue
    [PSCustomObject]@{
        Port        = $_.LocalPort
        State       = $_.State
        PID         = $_.OwningProcess
        ProcessName = $proc.ProcessName
        Path        = $proc.Path
    }
} | Format-Table -AutoSize
```

- **No output** = the port is free ✅ — you're good to launch.
- **Output appears** = something is already using the port . You can either:
  1. **Kill the process:** `Stop-Process -Id <PID> -Force` (replace `<PID>` with the number shown).
  2. **Change the port:** Edit `C4_GUI_PORT` in your `.env` file to a different value (e.g., `65004`).

> **Tip:** Replace `65003` in the command above with whatever port you have configured in `.env`.

### 🔄 Automatic Token Renewal
Control4 authentication tokens expire every 24 hours. This application features **background auto-renewal**. If a token expires, the system silently catches the error, re-authenticates, and retries. You will never need to manually restart the app.

###  Mobile & Local Network Access
The server listens on `0.0.0.0`, allowing access from smartphones, tablets, or other PCs on your local Wi-Fi.
1. Find your PC's local IP address (e.g., `192.168.1.50`).
2. Navigate to `http://192.168.1.50:65003` on your mobile device.
3. **Pro Tip:** Tap the Chrome menu and select **"Add to Home screen"** to install it as a full-screen web app!

### 🛡️ Smart UI Features
- **Smart Shutdown Button:** Hidden on mobile devices to prevent accidental server shutdowns.
- **Mobile Setup Restriction:** Setup controls are hidden on mobile to keep the interface clean.
- **Version Tag:** A small tag in the bottom-right corner (e.g., `v260915 | License valid till Jan 01, 2027`) tracks the version and beta status.

### 🔒 Security & File Locations
- **Never share your `.env` file** — it contains your Control4 credentials.
- The `.exe` looks for config files in the **same folder** as itself. If you move the `.exe`, you must move the `.env` and `dashboard_config.json` with it.
- The `templates/dashboard.html` file is now **embedded inside the .exe** and do not need to be distributed separately.

### 🔄 Updates
- When a new version of `C4DashboardToolexp_xxxxxx.exe` is released, simply replace the old `.exe` with the new one. Keep your existing `.env` and `dashboard_config.json` files.

---

## 🛠️ Troubleshooting

| Issue | Solution |
|-------|----------|
| **"Access Denied" / Shows Fingerprint** | The beta period (ending Jan 1, 2027) has ended, or the license check failed. Check the console logs for detailed error information. Paste a valid key into `.env` and click **🔄 Re-check License** on that screen. If the date has passed and you have no key, contact the developer. |
| **"Authentication failed"** | Handled automatically via background renewal. If it persists, check your credentials in `.env`. |
| **"dashboard.html is missing"** | The `.exe` cannot find its embedded UI files. Ensure you downloaded the complete package and have the latest version. |
| **"Port already in use"** | Another application or a second instance of C4DashboardTool is occupying the port. Run the **PowerShell port check** from the [Important Notes](#-check-that-your-port-is-free-before-launching) section above to identify and stop the conflicting process, or change `C4_GUI_PORT` in `.env` to a different port (e.g., `65004`). |
| **Cannot connect from phone** | Ensure your phone and PC are on the same Wi-Fi. Allow `C4DashboardTool.exe` through Windows Firewall. |
| **Widgets show "ERR"** | The controller may be unreachable. Check your network connection and `C4_HOST` IP address. |
| **License verification failed in console** | Check the detailed console logs for specific error reasons (empty key, invalid key, expired key, hardware mismatch, missing public_key.pem). |
| **New license key not recognized** | Click **🛡️ Check License** in Setup Mode (or **🔄 Re-check License** on the Access Denied screen) to force a live re-read of `.env` — no restart needed. The popup and the console logs show the detailed verification reason. |

---

## 💻 System Requirements

- **OS:** Windows 10 or Windows 11 (64-bit)
- **Network:** Access to your Control4 controller on the local network
- **Browser:** Any modern browser (Chrome, Firefox, Edge, Safari)

---

## ⚖️ Disclaimer

This project is **unofficial** and not affiliated with, endorsed by, or supported by Control4 Corporation. Use at your own risk. The Director API is intended for integration partners; ensure compliance with your local smart home policies and network security standards.

---

## 💡 Tips

- **Run only one instance** of `C4DashboardTool.exe` at a time. A second instance will fail to start because the port is already occupied by the first. Use the [PowerShell port check](#-check-that-your-port-is-free-before-launching) if you're unsure whether an instance is already running.
- **Firewall:** If other devices can't connect, allow `C4DashboardTool.exe` through Windows Firewall for Private networks.
- **Performance:** Keep the number of active Textbox/Combo widgets reasonable to minimize polling load on your Control4 controller.

---

## 💡 Thanks to ->>

Inspired by the brilliant work of #lawtancool and his predecessors. Uses some code from https://github.com/lawtancool/pyControl4. Made by Qwen AI under human supervision.

---

💡 Alternative way to run the application
DOCKER image — visit [andebox/c4dashboardtoolexp](https://hub.docker.com/r/andebox/c4dashboardtoolexp) to get an image.



## 📄 License

Free for personal use during the Beta period (valid until Jan 1, 2027). The application includes a secure licensing framework designed for authorized usage post-Beta.

---
