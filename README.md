# TPV Post-Assessment Forensic Laptop Audit

Official cross-platform proctoring forensic audit toolset for Windows and macOS.

## Downloads

| Platform | Download Package | Quick Instructions |
| :--- | :--- | :--- |
| **Windows** | [📥 **Download `Audit_Windows.zip`**](https://github.com/Hello9119-ai/Audit-/raw/main/Audit_Windows.zip) | 1. Extract `Audit_Windows.zip`<br>2. Double-click **`Audit.exe`**<br>3. Enter hours (or press **Enter** for default: 2) |
| **macOS** | [📥 **Download `Audit_Mac.zip`**](https://github.com/Hello9119-ai/Audit-/raw/main/Audit_Mac.zip) | 1. Extract `Audit_Mac.zip`<br>2. Double-click **`Audit.command`** (or `Audit.app`)<br>3. Enter hours (or press **Enter** for default: 2) |

---

## Invigilator 5-Second Checklist

The tool performs local, read-only system forensic checks across 5 core compliance areas:

1. **Screen Mirroring / Display Cloning**: Detects active duplicate coordinate clones, virtual display drivers, and hardware HDMI capture dongles.
2. **Actual Screen Share / Remote Control Session**: Detects confirmed active or logged screen sharing sessions (**AirPlay, Apple Screen Sharing / VNC, FaceTime / Messages SharePlay, AnyDesk, TeamViewer, Zoom CptHost, and WebRTC browser streaming**) with exact start/end timestamps, total duration, and remote partner/client proof.
3. **Screen Overlay & Laser Pointer Detection**: Identifies virtual laser pointer or cursor highlighting tools (e.g. Presentify, CursorPro, ProMouse) that render moving red dots or screen overlays.
4. **AI Website / Solver Visited & Extensions**: Analyzes browser history timelines with exact timestamps, dwell time, user account email, and specific problem/chat URLs. Audits browser extensions for sideloaded test-cheating tools.
5. **Browser History Wiped / Tampered**: Recovers deleted AI visits from the Omnibox shortcut cache.

