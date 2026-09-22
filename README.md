# Hey, I'm Nephren 👋

🇫🇷 [Version française](README_FRENCH.md)

Bonjour à tous ; hello everyone. I build PowerShell tools for Windows 11 — security audits, privacy hardening, and system maintenance — for people who want to know *exactly* what a script touched on their machine, not just trust that it "did something."

Every script here follows the same house rules: a built-in `-SelfTest` mode that validates the script's own logic before it ever runs for real, no unattended auto-elevation, and code signing where it matters. If a script tells you your system is healthy, it's because a documented threshold said so — not a hunch.

---

### 🧰 What's here

| Repository | What it does |
|---|---|
| 🌶️ [**SpicyCheck**](https://github.com/NephVx2/SpicyCheck) | One-command Windows 11 tune-up — 16-point health diagnostic, cleanup, bilingual FR/EN DISM/SFC/BCD repair, disk optimization, HTML dashboard. 36-assertion self-test. |
| 🩺 [**Check-Security**](https://github.com/NephVx2/Check-Security) | Read-only Windows 11 security audit — 22 sections (firewall, BitLocker, Defender, TLS/SCHANNEL, VBS, certificates...), category-weighted scoring, regression alerts across runs, section-filterable via `-Category`. 48-assertion self-test. |
| 🔒 [**Harden-TLS**](https://github.com/NephVx2/Harden-TLS) | Your PC still accepts TLS 1.0 and a stack of other encryption relics from the 1990s — one script closes it all for good: protocols, ciphers, hashes, Diffie-Hellman, .NET Strong Crypto. Checks itself before touching anything, one-click undo. 17-assertion self-test. |
| 🛰️ [**Block-Telemetry**](https://github.com/NephVx2/Block-Telemetry) | Blocks telemetry via the hosts file — 228 domains, 15 categories (Microsoft, Edge, Copilot, Adobe, Google, Brave and more). Hard-coded whitelist, dry-run mode, integrity checker. 8-assertion self-test. |
| 🦁 [**Brave-Debloat**](https://github.com/NephVx2/Brave-Debloat) | Applies 53 Brave Group Policy settings for privacy and security — backup/restore, conflict detection, HTML reporting. 21-assertion self-test. |
| 🧹 [**Windows-Preflight-Cleaner**](https://github.com/NephVx2/Windows-Preflight-Cleaner) | Self-contained maintenance script — 46+ system/app caches, logs, temp files and WinSxS via DISM, DNS flush, Recycle Bin. Dry-run mode. 17-assertion self-test. |
| 🧭 [**Toolbox-SystemCommands**](https://github.com/NephVx2/Toolbox-SystemCommands) | Point-and-click access to 145 Windows commands across 9 categories — search, favorites, confirmation prompts on risky commands, 47-assertion self-test. Ships as separate English and French versions, each self-contained. |

---

### 🎨 Also here

Not PowerShell, but scratched a different itch:

- 🦅 [**fastfetch-ricing**](https://github.com/NephVx2/fastfetch-ricing) — a Fastfetch config for Windows 11 / PowerShell Sixel terminals, grouped Hardware/Software/Session/Uptime sections, progress bars, and a custom logo slot.
- 🎧 [**Spicetify-tui**](https://github.com/NephVx2/Spicetify-tui) — a terminal-style Spicetify theme for Spotify, panel labels, ASCII banner, TokyoNight by default.

---

### 🛠️ How these scripts are built

- **Self-tested** — most scripts ship with a `-SelfTest` (or equivalent) mode: dozens of internal assertions confirming required binaries, cmdlets, and functions all work *before* anything touches your system.
- **Transparent scoring** — health/security statuses are always backed by a documented, explicit threshold. No black-box "trust me."
- **Bilingual where it matters** — French and English are both first-class; detection logic that reads system output (DISM, SFC...) is checked against both languages, not just English.
- **Signed where noted** — some scripts carry a personal, self-signed code-signing certificate (check the bottom of the `.ps1` for a `SIG # Begin signature block`); others aren't signed at all. Either way, see below for what that means when you run one.
- **Admin-aware, not admin-hungry** — scripts that need elevation require it explicitly; none of them silently self-elevate.

---

### 🔓 Running a downloaded script

Any `.ps1` you download from these repos will be tagged by Windows as coming from "the Internet zone" (the Mark of the Web). Under the common `RemoteSigned` execution policy, that tag blocks the script from running — **whether or not it's signed**:

- **Signed scripts** here use a personal, self-signed certificate. Its trust root isn't installed on your machine, so — unlike a certificate from a public certificate authority — it won't make Windows treat the file as coming from a "trusted publisher." The signature mainly proves the file wasn't altered after I signed it, not that your machine should trust it by default.
- **Unsigned scripts** hit the same Internet-zone block, for the simpler reason that there's no certificate to even attempt trusting.

The fix is identical in both cases — pick whichever you're comfortable with:

```powershell
# Option A - remove the "downloaded from the Internet" flag (one-time, permanent)
Unblock-File .\script-name.ps1

# Option B - bypass the policy for a single run, without touching the file
powershell -ExecutionPolicy Bypass -File .\script-name.ps1
```

**Option C — no PowerShell needed:** right-click the `.ps1` file → *Properties* → on the *General* tab, check **"Unblock"** next to the security notice ("This file came from another computer...") → *OK*. This does exactly the same thing as `Unblock-File`, just through the file explorer.

If PowerShell says instead that running scripts is disabled on this system (the Windows default policy is `Restricted`), Option B above still works as-is — it bypasses whatever the current policy is for that one run. To fix it more permanently, allow scripts for your account first (this changes the policy for your account only, not machine-wide):

```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

Still blocked after all of this? See the [step-by-step guide](https://github.com/NephVx2/Script-blocked-Look-at-this) for a more detailed walkthrough, including SmartScreen/Defender warnings.

`Unblock-File` (or the checkbox above) only clears the flag on that specific file — it doesn't change your system's execution policy or affect any other script. Read a script before unblocking and running it, especially as Administrator.

---

### 🖱️ Desktop shortcut for scripts you use often

Most of these are one-off scripts you run from a PowerShell prompt when needed. [**Toolbox-SystemCommands**](https://github.com/NephVx2/Toolbox-SystemCommands) is different — it's a GUI you might open several times a day, so it's worth a proper double-click shortcut instead of right-clicking the `.ps1` and choosing "Run with PowerShell" every time (which briefly flashes a console window and leaves it open behind the GUI).

1. Right-click the Desktop → **New → Shortcut**.
2. For the location, paste one of the two commands below (adjust the script path to wherever you placed it) — pick whichever matches what's installed on the machine:

   **Windows PowerShell 5.1** (built into every Windows install):
   ```
   powershell.exe -NoProfile -ExecutionPolicy Bypass -WindowStyle Hidden -File "C:\Scripts\Toolbox\Toolbox-SystemCommands.ps1"
   ```

   **PowerShell 7+** (only if installed separately):
   ```
   pwsh.exe -NoProfile -ExecutionPolicy Bypass -WindowStyle Hidden -File "C:\Scripts\Toolbox\Toolbox-SystemCommands.ps1"
   ```

   | Flag | Why |
   |---|---|
   | `-NoProfile` | Skips loading your PowerShell profile, so the script starts faster and isn't affected by anything custom in it |
   | `-ExecutionPolicy Bypass` | Applies only to this one process — lets the script run even if the system's default execution policy would otherwise block it, without changing that policy machine-wide |
   | `-WindowStyle Hidden` | Suppresses that first process's own console window, so only the script's GUI appears |

3. Name the shortcut, then finish.
4. *(Optional)* Right-click the new shortcut → **Properties** → **Change Icon...** for something more recognizable than the default PowerShell icon.

The same shortcut pattern works for any other script here you plan to launch by double-click regularly — just point `-File` at that script instead. Note that `-WindowStyle Hidden` only hides the console window; it never suppresses a UAC elevation prompt for scripts that need admin rights.

---

### 📬 Get in touch

Found a bug, or a French Windows message my scripts don't recognize yet? Open an issue on the relevant repo — that's exactly the kind of report that makes these tools better.

<sub>PowerShell · Windows 11 · Security & Privacy · Self-tested, signed, bilingual.</sub>
