# Exam Lockdown Tool

A toggleable internet restriction utility for Windows education devices. This tool uses a **black-hole proxy** to restrict traffic while locking the Windows UI to prevent tampering.

---

## 🚀 Core Features

*   **Black-Hole Proxy:** Redirects all traffic to a non-existent local port ($127.0.0.1:9999$).
*   **Whitelist Bypass:** Supports domain and subdomain whitelisting (e.g., `exam.org`).
*   **UI Hardening:** Uses Registry-based Group Policy to lock the Windows Proxy settings menu.
*   **Dead Man's Switch:** Automatic restoration via a Windows Scheduled Task to prevent permanent lockouts.
*   **Backup/Restore:** Saves original proxy settings to a JSON file and restores them upon unlocking.

---

## ⚙️ Configuration

You can edit the `$CONFIG` object at the top of the script or use the **"Edit Configuration"** button in the GUI.

| Variable | Description |
| :--- | :--- |
| **WhitelistDomain** | Comma-separated domains allowed during exams. |
| **DeadManHours** | Time (in hours) before the system auto-restores. |
| **BlackHoleProxy** | The fake proxy address (default `127.0.0.1:9999`). |
| **DataDir** | Storage for logs and proxy backups (`ProgramData`). |

---

## 🛠 Usage Instructions

### 1. Requirements
*   **OS:** Windows 10 or 11.
*   **Version:** PowerShell 5.1+.
*   **Permissions:** Must be run as **Administrator**.

### 2. Running the Tool
1.  Right-click the script and select **Run with PowerShell**.
2.  **To Lock:** Click `ACTIVATE LOCKDOWN`. The status turns **RED**.
3.  **To Unlock:** Click `RESTORE SYSTEM`. This restores original settings.

### 3. Automation (Dead Man's Switch)
If the device is not manually unlocked, the script triggers the `-AutoRestore` switch after the configured time limit. No more "oops, I locked the whole lab forever."

---

## 📝 Technical Notes

*   **Registry Path:** `HKCU:\Software\Microsoft\Windows\CurrentVersion\Internet Settings`
*   **Policy Path:** `HKLM:\SOFTWARE\Policies\Microsoft\Internet Explorer\Control Panel`
*   **Logs:** Check `$env:ProgramData\ExamLockdown\lockdown.log` for activity traces.
