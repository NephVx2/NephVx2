# Hey, I'm Nephren 👋

🇫🇷 [Version française](README_FRENCH.md)

Bonjour à tous ; hello everyone. I build PowerShell tools for Windows 11 — security audits, privacy hardening, and system maintenance — for people who want to know *exactly* what a script touched on their machine, not just trust that it "did something."

Every script here follows the same house rules: a built-in `-SelfTest` mode that validates the script's own logic before it ever runs for real, no unattended auto-elevation, and code signing where it matters. If a script tells you your system is healthy, it's because a documented threshold said so — not a hunch.

---

### 🧰 What's here

| Repository | What it does |
|---|---|
| 🌶️ [**SpicyCheck-v7.2**](https://github.com/NephVx2/SpicyCheck-v7.2) | One-command Windows 11 tune-up — 16-point health diagnostic, cleanup, bilingual FR/EN DISM/SFC/BCD repair, disk optimization, HTML dashboard. 36-assertion self-test. |
| 🩺 [**Windows-Check-Security**](https://github.com/NephVx2/Windows-Check-Security) | Read-only Windows 11 security audit — 22 sections (firewall, BitLocker, Defender, TLS, VBS, certificates...), category-weighted scoring, regression alerts across runs. |
| 🧹 [**Windows-Preflight-Cleaner**](https://github.com/NephVx2/Windows-Preflight-Cleaner) | Self-contained maintenance script — 46+ system/app caches, logs, temp files and WinSxS via DISM, DNS flush, Recycle Bin. Dry-run mode included. |
| 🔒 [**Harden-TLS**](https://github.com/NephVx2/Harden-TLS) | Your PC still accepts TLS 1.0, deprecated since 2021 — one script closes that door for good, checks itself before touching anything, never rewrites what's already fixed. |
| 🛰️ [**Windows-Block-Telemetry**](https://github.com/NephVx2/Windows-Block-Telemetry) | Blocks telemetry across Microsoft, AMD, Adobe, Spotify, Brave, Firefox, Google, Discord, Steam and more, sorted by category. |
| 🦁 [**Brave-debloat**](https://github.com/NephVx2/Brave-debloat) | Interactive cleanup of unnecessary Brave options to tighten security and privacy. |
| 🧭 [**Toolbox-Commands**](https://github.com/NephVx2/Toolbox-Commands) | A GUI toolbox plus a separate command catalog — drop them in the same folder to launch a wide range of Windows commands from one window. |

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

The fix is identical in both cases:

```powershell
# Option A - remove the "downloaded from the Internet" flag (one-time, permanent)
Unblock-File .\script-name.ps1

# Option B - bypass the policy for a single run, without touching the file
powershell -ExecutionPolicy Bypass -File .\script-name.ps1
```

`Unblock-File` only clears the flag on that specific file — it doesn't change your system's execution policy or affect any other script. Read a script before unblocking and running it, especially as Administrator.

---

### 📬 Get in touch

Found a bug, or a French Windows message my scripts don't recognize yet? Open an issue on the relevant repo — that's exactly the kind of report that makes these tools better.

<sub>PowerShell · Windows 11 · Security & Privacy · Self-tested, signed, bilingual.</sub>
