# Research & Publications — Bhargav Rathod

Threat intelligence reports, research papers, and publications.

---

## Publications

| Date | Title | Authors | Publisher | Link |
|---|---|---|---|---|
| Jun 20, 2026 | ClickFix Campaign Delivers macOS Infostealer via DMG | Manbendra Satpathy, **Bhargav Rathod**, Shazan Khaja, Veronika Senderovych | Palo Alto Networks Unit 42 | [View](https://github.com/PaloAltoNetworks/Unit42-timely-threat-intel/blob/main/2026-06-20-ClickFix-campaign-delivers-macOS-infostealer-via-DMG.txt) |

---

## Books

| Year | Role | Title | Authors | Publisher | ISBN |
|---|---|---|---|---|---|
| 2026 | Technical Reviewer | [Android and iOS Mobile Forensics: Leveraging Blockchain, Machine Learning, and Deep Learning for Digital Investigations](https://link.springer.com/book/10.1007/979-8-8688-1748-9) | Ravi Sheth, Keshav Kaushik, Chandresh Parekha, Narendrakumar Chayal | Apress, Berkeley CA (Springer Nature) | Softcover: [979-8-8688-1747-2](https://link.springer.com/book/10.1007/979-8-8688-1748-9) / eBook: [979-8-8688-1748-9](https://link.springer.com/book/10.1007/979-8-8688-1748-9) |
| 2025 | Technical Reviewer | [Advanced Malware Analysis and Intelligence](https://in.bpbonline.com/products/advanced-malware-analysis-and-intelligence) | Mahadev Thukaram, Dharmendra T | BPB Publications, India | Paperback: [9789365899504](https://in.bpbonline.com/products/advanced-malware-analysis-and-intelligence) / eBook: 9789365890709 |
| 2021 | Book Editor | [A Guide to Forensics and Indian Law: Investigating Crimes in the 21st Century](https://www.google.co.in/books/edition/The_Guide_to_Forensics_Indian_Law/sdRpzgEACAAJ?hl=en) | Anuj Kumar, Mahipal Singh Sankhla, Kapil Parihar | Legal Desire Publications, Dept. of Forensic Science & Criminal Investigation | [978-0-578-89799-8](https://www.researchgate.net/publication/350947506_Guide_To_Forensics_Indian_Law_Investigating_Crimes_in_21st_Century) |

---

## Projects & Supervision

| Year | Role | Title | Student | Abstract |
| --- | --- | --- | --- | --- |
| 2025 | Mentor / Supervisor | Claude AI Forensic Artefact Script | Saaya Rupesh, Anousha Samuel, Kesia Ann Wilson (UG Students, Kristu Jayanti College, Bangalore) | Guided students to develop a Python-based forensic automation tool that collects Claude AI artifacts on Windows. Tool published on GitHub as part of the WiCyS Student Chapter Mentorship Program. |
| 2024 | Co-Guide | PowerShell Script Analysis Automation | Rishika Jain (PG Minor Project, Rashtriya Raksha University — Gujarat Campus) | Analysis of obfuscated PowerShell scripts using static and dynamic tools (PSDecode, PowerDecode, StoQ Framework). Evaluates de-obfuscation techniques against Base64 encoding, string encryption and control flow alteration, with proposals for a unified scalable solution integrating threat intelligence. |
| 2024 | Co-Guide | macOS Malware Analysis: A Critical Review of the Literature | Roshini John (PG Minor Project, Rashtriya Raksha University — Gujarat Campus) | — |
| 2024 | Co-Supervisor | Drinik Demystified: A Detailed Examination of Android Malware Patterns, Detection Techniques, and Defensive Measures |Ashra Hakim (PG Dissertation, Centurion University of Technology and Management, Odisha) | Analysis of Drinik Android malware targeting Indian taxpayers using a novel VM-WSA methodology combining VMware Workstation Pro, API Monitor, Process Monitor, TCPView and Windows Subsystem for Android to forensically examine permissions, communication patterns and behavioral indicators. |
| 2023 | Researcher | [Windows Subsystem for Android Forensics](https://www.sans.org/presentations/investigating-a-wsa-endpoint) | Debasis Parida | Research carried out on Windows Subsystem for Android (WSA) and presented at SANS DFIR Summit 2023. |

---

## 2026 — ClickFix Campaign Delivers macOS Infostealer via DMG

| Field | Details |
|---|---|
| **Publisher** | Palo Alto Networks Unit 42 |
| **Date** | June 20, 2026 |
| **Authors** | Manbendra Satpathy, Bhargav Rathod, Shazan Khaja, Veronika Senderovych |
| **Malware Family** | AMOS (Atomic macOS Stealer) — C++ Odyssey variant |
| **Architecture** | Universal Mach-O (Intel x64 + ARM64) |
| **Initial Access** | Fake CAPTCHA page → Terminal paste → silent DMG mount via `hdiutil attach -nobrowse` |
| **Staging Directory** | `~/.hlpr/` |
| **Persistence** | LaunchAgent `~/Library/LaunchAgents/com.hlpr.agent.plist` |
| **Config Encryption** | XOR, 8-byte rotating key: `a9048cf1c9d113b6` |
| **String Encryption** | SIMD XOR, 32-byte key: `8111edf01ac6cb5c77e249d4e84fd92a85b5e89c2e2bef92fbe00b6f1cc2aa8e` |
| **Build Info** | Build ID: 123 \| Campaign: 25 \| Build name: noname3 |
| **C2 Endpoints** | `/api/reports/upload` \| `/api/agent/download` \| `/api/download/app-bundle` |

### Capabilities

| Category | Detail |
|---|---|
| **Credential Phishing** | Fake osascript System Preferences dialog; validated via `dscl . -authonly` |
| **Browser Theft (Chromium)** | Arc, Brave, Chrome, Edge, Opera, Vivaldi, Yandex, CocCoc — cookies, login data, web data |
| **Browser Theft (Firefox)** | LibreWolf, SeaMonkey, Tor Browser, Waterfox, Zen — cookies.sqlite, logins.json |
| **Wallet Extensions** | 201 browser crypto wallet extension directories |
| **Standalone Wallets** | Electrum, Exodus, Atomic, Bitcoin Core, Litecoin Core, DashCore, Guarda, Dogecoin, Binance, TonKeeper, Wasabi, Electron Cash, Electrum-LTC |
| **Messaging** | Telegram, Discord (incl. keychain key via discord Safe Storage) |
| **Additional Collection** | Apple Notes, Safari cookies, macOS login keychain, user documents (PDF/TXT/RTF) |
| **Exfiltration** | `curl POST` to C2 `/api/reports/upload` with `user_id` and `build_tag` params |
| **Supply-Chain Hijack** | Trojanizes Ledger Live and Trezor Suite in `/Applications` via `ditto -x -k` |

### Indicators of Compromise

#### Network

| Type | Indicator |
|---|---|
| IP | `178.16.52[.]101` |
| IP | `196.251.107[.]171` |
| Domain | `svs-verificationdate[.]beer` |
| Domain | `fewfwfwfwfwf[.]info` |
| URL | `hxxp[:]//svs-verificationdate[.]beer/f0038a5f46720da5982b6984ceef10cf99359432e102b12a0b0657498d36f670` |
| URL | `hxxps[:]//fewfwfwfwfwf[.]info` |
| URL | `hxxp[:]//196.251.107[.]171:3000` |

#### File Hashes

| File | SHA-256 |
|---|---|
| s.01M0td.dmg | `25b6fc4f9c54a28ba7bfc4dfeafb62c99b59ea6f0d17679219b876b321965095` |
| NNApp.app (bundle) | `067ad6221b2224d5cdb64e51c5516132d820cf4d7edf9ec170643943e79c04b7` |
| Mach-O x64 | `d6f479736ba55d3c4e895c4940d035cf772f3192fb8dc496f09a801aed16d970` |
| Mach-O ARM64 | `833008c03d40422192051584d829d730497108bef31751cceb0cc043dd96bbfb` |

#### Host Artifacts

| Type | Path |
|---|---|
| Staging directory | `~/.hlpr/` |
| Ownership file | `~/.hlpr/User Name.txt` |
| System profile | `~/.hlpr/System Information.txt` |
| Persistence | `~/Library/LaunchAgents/com.hlpr.agent.plist` |
| Initial download | `/private/tmp/s.01M0td.dmg` |
| Mounted volume | `/Volumes/NNApp/NNApp.app` |
| Bundle identifier | `com.utils.nnapp` |

---

## Training & Guest Lectures

| Year | Role | Title | Organiser |
|---|---|---|---|
| 2025 | Mentor | [WiCyS India Student Chapter Mentorship Program](https://www.linkedin.com/company/wicys-india-affiliate/) | Women in CyberSecurity (WiCyS) India — Kristu Jayanti College, Bangalore (6-month program) |
| 2025 | Guest Speaker | Overview of Digital Forensics | One-week Training Program on Digital Forensics & Incident Response, Rashtriya Raksha University — Pasighat Campus |


---

## License

© Bhargav Rathod. All rights reserved.
