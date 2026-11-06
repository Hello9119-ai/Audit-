# TPV Post-Assessment Forensic Laptop Audit

Official cross-platform proctoring forensic audit toolset for Windows and macOS.

## Downloads

| Platform | Download Package | Quick Instructions |
| :--- | :--- | :--- |
| **Windows** | [📥 **Download `Audit_Windows.zip`**](https://github.com/Hello9119-ai/Audit-/raw/main/Audit_Windows.zip) | 1. Extract `Audit_Windows.zip`<br>2. Double-click `Run_Audit.bat`<br>3. Press **Enter** for default 2-hour audit |
| **macOS** | [📥 **Download `Audit_Mac.zip`**](https://github.com/Hello9119-ai/Audit-/raw/main/Audit_Mac.zip) | 1. Extract `Audit_Mac.zip`<br>2. Double-click `Audit.app` (or `Audit_Mac.command`)<br>3. Press **Enter** for default 2-hour audit |

---

## Invigilator 5-Second Checklist

The tool performs local, read-only system forensic checks across 5 core compliance areas:

1. **Screen Mirroring / Display Cloning**: Detects active duplicate coordinate clones, virtual display drivers, and HDMI capture dongles.
2. **Remote Screen Share / Control Session**: Identifies active or recorded remote desktop sessions (Apple Screen Sharing, Windows RDP, AnyDesk, TeamViewer) with exact start/end timestamps and total duration.
3. **Live AI Windows Open Right Now**: Checks for active foreground AI solver windows (ChatGPT, Gemini, Claude, DeepSeek).
4. **AI Website / Solver Visited**: Analyzes browser history timelines with exact timestamps, dwell time, user account email, and specific problem/chat URLs.
5. **Browser History Wiped / Tampered**: Recovers deleted AI visits from the Omnibox shortcut cache.
