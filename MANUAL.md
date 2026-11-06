# GGTK User Manual

GGTK is an **SSH / SFTP / serial console** client in the style of MobaXterm, for Mac and Windows.
This manual covers version **1.0.1**.

**Contents**
1. [Install](#1-install)
2. [The main window](#2-the-main-window)
3. [Connect over SSH](#3-connect-over-ssh)
4. [Serial console](#4-serial-console)
5. [Sessions and folders](#5-sessions-and-folders)
6. [Tabs and split panes](#6-tabs-and-split-panes)
7. [Copy, paste and search](#7-copy-paste-and-search)
8. [SFTP file transfer](#8-sftp-file-transfer)
9. [Logs and Export](#9-logs-and-export)
10. [Settings (dark theme, fonts …)](#10-settings)
11. [Let Claude Code run commands](#11-let-claude-code-run-commands)
12. [All keyboard shortcuts](#12-all-keyboard-shortcuts)
13. [Troubleshooting](#13-troubleshooting)

---

## 1. Install

Download from **[Releases](https://github.com/THEPPITUKK/ggtk-releases/releases/latest)** → **Assets**.

### Mac (Apple silicon M1 or later, macOS 13 or later)
1. Download `GGTK_<version>_aarch64_team.dmg` and double-click it.
2. Drag **GGTK** onto **Applications** (delete any older copy first).
3. Open GGTK. If macOS blocks it, click **Done** → **System Settings → Privacy & Security** → scroll down → **Open Anyway** → enter your Mac password.
4. If it says "GGTK is damaged", open Terminal and run:
   ```
   xattr -dr com.apple.quarantine /Applications/GGTK.app
   ```

### Windows 10 / 11 (64-bit)
1. Download `GGTK_<version>_x64-setup.exe`.
2. If Edge says "isn't commonly downloaded": click **⋯** on the file → **Keep** → **Show more** → **Keep anyway**.
3. Run the file. On the blue "Windows protected your PC" screen: **More info** → **Run anyway**.
4. Click Next to the end (no admin rights needed) and start GGTK from the Start menu.

> These warnings appear because the app is not code-signed yet. It is not a virus.

### First launch
Click **Agree** on the licence (team use only, do not redistribute). You can read it again under Settings → License.

**Updating:** install the new version over the old one. Your sessions and saved passwords are kept.

---

## 2. The main window

| Area | Where | What it does |
|---|---|---|
| **Toolbar** | Top | Session (new) · Quick (quick connect) · Serial · Split · Import · Sessions (show/hide sidebar) · Settings |
| **Sidebar** | Left | **Sessions** tab (saved hosts) and **SFTP** tab (files on the server) |
| **Terminal tabs** | Centre | One terminal per connection |
| **Status bar** | Bottom | Connection state, server CPU / RAM / disk / network (Linux), Export, Reconnect, Send Break, Claude Code ✦ icon |

Shortcuts in this manual are written **Mac / Windows**, e.g. ⌘T / Ctrl+Shift+T.

---

## 3. Connect over SSH

### Quick connect (not saved)
Click **Quick** (⌘T / Ctrl+Shift+T) → enter Host, Port and User → choose a login method → Connect.

### Saved session
Click **Session** (⌘N / Ctrl+Shift+N) and fill in:

| Field | What to enter |
|---|---|
| Host | IP address or host name |
| Port | Usually 22 |
| User | Your user name on the server |
| Login with | **Password** · **Private key file** (pick the key) · **ssh-agent** |
| Name | Name shown in the list |
| Folder | Folder to keep it in (empty = top level) |
| Tab colour | Colour of the tab, handy for marking important hosts |
| Log output to a file | Log just this session (all sessions are logged by default, see section 9) |

Click **Save**, then **double-click** the session in the sidebar to connect.

### Passwords
- Passwords are **never stored in the session**. GGTK asks when you connect.
- Tick **Remember** in the password prompt to keep it in the **Keychain** (Mac) or **Windows Credential Manager** (Windows), so you are not asked next time.
- Splitting a pane or opening another tab to the same host reuses the password you typed; it is forgotten when you quit.

### First connection: host key
The first time you connect to a host, GGTK asks you to **Trust** its host key. Check it is the machine you meant, then click Trust.
If you ever get a warning that the **key has changed** and the host was not reinstalled, stop and ask whoever runs that host.

### Connection problems
- If the network drops, GGTK **reconnects automatically** (can be turned off in Settings).
- Click **Reconnect** in the status bar, or press ⌘R / Ctrl+Shift+R.
- Older switches and routers work too (SHA-1 key exchange / CBC ciphers are supported).

### Import from `~/.ssh/config`
Click **Import**. GGTK reads the Host entries in `~/.ssh/config` (Windows: `C:\Users\<you>\.ssh\config`) and creates sessions for them.

---

## 4. Serial console

1. Plug in the USB-serial cable.
2. Click **Serial** in the toolbar.
3. **Serial port**: pick the port (Mac: `/dev/cu.usbserial-…`, Windows: `COM3`, `COM4` …). Click **Refresh** if it is missing.
4. Set the line settings. Most switches use **9600, 8, None, 1, None** (9600 8N1):
   Speed (baud) · Data bits · Parity · Stop bits · Flow control.
5. Save, double-click to connect, then press Enter once to get a prompt.

- **Send Break** (status bar or Shell menu) for ROM / password-recovery mode.
- Unplug and replug the cable and GGTK reconnects by itself.
- Windows: if no port shows up, install the cable's driver (Prolific / FTDI / CH340 …) and check the COM number in Device Manager → Ports.

> ⚠️ Don't type Thai (or other non-ASCII) text into a serial console. Devices can't read it.

---

## 5. Sessions and folders

- **Right-click a session:** Connect · Edit… · Duplicate · Delete…
- **Right-click a folder:** New Session Here… · New Folder Inside… · Rename… · Delete Folder
- **Right-click empty space:** New Session… · New Folder…
- **Drag** a session onto a folder to move it. Hover over a closed folder for a moment to open it; press Esc to cancel.
- The **search** box at the top of the sidebar matches names and IPs.
- Show / hide the sidebar: ⌘B / Ctrl+Shift+B

---

## 6. Tabs and split panes

| Action | Mac | Windows |
|---|---|---|
| Split right | ⌘D | Ctrl+Shift+D |
| Split down | ⌘⇧D | Ctrl+Shift+E |
| Next pane | ⌘] | Ctrl+Shift+] |
| Close pane / tab | ⌘W (or the ✕ at the top right of a pane) | Ctrl+Shift+W |
| Next / previous tab | ⌘⇧] / ⌘⇧[ | Ctrl+Tab / Ctrl+Shift+Tab |
| Go to tab 1–9 | ⌘1 … ⌘9 | Ctrl+1 … Ctrl+9 |

A split opens another session to the same host without asking for the password again.

---

## 7. Copy, paste and search

| | Mac | Windows |
|---|---|---|
| Copy | Select text → ⌘C | Select text → **Ctrl+C** (or Ctrl+Shift+C) |
| Paste | ⌘V | **Ctrl+V** (or Ctrl+Shift+V) |
| Interrupt (^C) | Ctrl+C | Ctrl+C **with nothing selected** |
| Open a link on screen | ⌘-click | Ctrl-click |
| Find | ⌘F | Ctrl+Shift+F |
| Clear screen | ⌘K | Ctrl+Shift+K |

**Keyword colours** (MobaXterm style): up/ok green · down/error red · warning yellow · IP addresses blue · MAC addresses purple. You can turn this off in Settings.
Logs and exports are plain text without these colours.

---

## 8. SFTP file transfer

When an SSH session connects, the **SFTP** panel opens on the left (can be turned off in Settings).

- **Upload:** drag files or folders from Finder / File Explorer into the panel, or right-click empty space → Upload Files… / Upload Folders…
- **Download:** right-click a file → **Download** (to Downloads) or **Download to…** (choose a folder). When done, click **Show in Finder / Explorer**.
- **Edit a file on the server:** right-click → **Edit in Text Editor**. It opens in TextEdit (Mac) / Notepad (Windows); every time you **Save**, GGTK uploads it back.
- More on right-click: Rename… · Permissions… (chmod) · **SHA256 Checksum** · Copy Path · Delete…
- Right-click empty space: New Folder… · Refresh
- Select several: Shift-click (range) · ⌘-click / Ctrl-click (one at a time)
- Delete the selection: ⌘⌫ (Mac) / Delete (Windows)
- Transfers are listed under the panel. Click ✕ to cancel; **Clear finished** tidies the list.

---

## 9. Logs and Export

- **Automatic logs:** every session is saved to `Documents/GGTK Logs` (change it under Settings → Log folder).
  To log only some sessions: Settings → untick "Save a log file of every session", then tick "Log output to a file" on the sessions you want.
- **Export:** the **Export** button in the status bar, or ⌘⇧S / Ctrl+Shift+S, saves everything in the current tab (all panes, including scrollback) as a .txt file. Handy for `show run` / `display current-configuration` output.

---

## 10. Settings

Open with the **Settings** button (⌘, / Ctrl+Shift+,).

| Setting | Meaning |
|---|---|
| **Theme** | **Match system** · **Dark** · **Light** |
| Font / Font size | Terminal font (quick size: ⌘= ⌘- ⌘0 / Ctrl+= Ctrl+- Ctrl+0) |
| Scrollback lines | How many lines you can scroll back |
| Keepalive (seconds) | How often to ping the server so the connection stays up |
| Log folder | Where log files go |
| Reconnect automatically | Reconnect when a connection drops |
| Colour keywords | Colour up/down/error/IP/MAC |
| Save a log file of every session | Log all sessions |
| Show server CPU, memory… | Server stats in the status bar (Linux only) |
| Show the SFTP file browser… | Open the SFTP panel on SSH connect |
| Let Claude Code use open sessions | See section 11 |

**Dark theme:** Theme → **Dark** → Save.
(Or switch the whole computer to dark mode: Mac = System Settings → Appearance; Windows = Settings → Personalization → Colors → Choose your mode.)

**Reset to defaults** restores all settings. The app version is shown at the bottom; include it when you report a bug.

---

## 11. Let Claude Code run commands

If you use [Claude Code](https://claude.com/claude-code), you can let it read the screen and run commands in your open sessions.

1. Settings → tick **Let Claude Code use open sessions** → **Save**.
2. Open Settings again and copy the command shown (`claude mcp add …`). Run it **once** in Terminal / PowerShell.
3. Start Claude Code and ask, e.g. "show me which interfaces are down on switch-core".

- **Every command needs your Allow click in GGTK.** No answer within 2 minutes = denied.
- The ✦ icon in the status bar shows the state (ready / connected / working).
- Untick the setting at any time to turn it off.

---

## 12. All keyboard shortcuts

| Command | Mac | Windows |
|---|---|---|
| New session | ⌘N | Ctrl+Shift+N |
| Quick connect | ⌘T | Ctrl+Shift+T |
| Split right / down | ⌘D / ⌘⇧D | Ctrl+Shift+D / Ctrl+Shift+E |
| Reconnect | ⌘R | Ctrl+Shift+R |
| Close | ⌘W | Ctrl+Shift+W |
| Find | ⌘F | Ctrl+Shift+F |
| Clear screen | ⌘K | Ctrl+Shift+K |
| Export text | ⌘⇧S | Ctrl+Shift+S |
| Show / hide sidebar | ⌘B | Ctrl+Shift+B |
| Settings | ⌘, | Ctrl+Shift+, |
| Font bigger / smaller / default | ⌘= / ⌘- / ⌘0 | Ctrl+= / Ctrl+- / Ctrl+0 |
| Next / previous tab | ⌘⇧] / ⌘⇧[ | Ctrl+Tab / Ctrl+Shift+Tab |
| Tab 1–9 | ⌘1–9 | Ctrl+1–9 |
| Next pane | ⌘] | Ctrl+Shift+] |

Shortcuts work even when a Thai keyboard layout is active.
**Why Windows needs Shift:** Ctrl+C / D / R / W / K belong to the shell and network devices (interrupt, logout, history search …), so GGTK leaves them to the terminal, just like Windows Terminal.

---

## 13. Troubleshooting

| Problem | Fix |
|---|---|
| Mac: "GGTK is damaged" | Run `xattr -dr com.apple.quarantine /Applications/GGTK.app` |
| Mac: blocked on first open | System Settings → Privacy & Security → Open Anyway |
| Windows: "Windows protected your PC" | More info → Run anyway |
| "No common Kex algorithm" / old switch won't connect | Report it on Discord with the device model |
| Asked for the password every time | Tick Remember in the password prompt |
| No serial port listed | Click Refresh · Windows: install the cable driver, check Device Manager · close other apps using the port (PuTTY, SecureCRT) |
| No CPU / RAM in the status bar | Only for Linux servers over SSH |
| No log file | Settings → tick "Save a log file of every session" and check Log folder |

**Bugs and questions:** Discord https://discord.gg/WG48jFrRgR (also under the Help menu).
Include the version (shown in Settings), Mac or Windows, what you did and what happened, and a screenshot. **Never paste passwords or customer IPs.**
