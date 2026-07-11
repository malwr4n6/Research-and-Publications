# Research & Publications — Bhargav Rathod

Threat intelligence reports, research papers, and publications.

---

## 2026

### ClickFix Campaign Delivers macOS Infostealer via DMG
**Publisher:** Palo Alto Networks Unit 42
**Date:** June 20, 2026
**Authors:** Manbendra Satpathy, Bhargav Rathod, Shazan Khaja, Veronika Senderovych
**Link:** [Unit 42 Timely Threat Intel](https://github.com/PaloAltoNetworks/Unit42-timely-threat-intel/blob/main/2026-06-20-ClickFix-campaign-delivers-macOS-infostealer-via-DMG.txt)

#### Summary
A new macOS ClickFix campaign uses a fake CAPTCHA page to trick users into installing malware. It instructs users to paste text into a Terminal command that silently downloads and mounts a malicious DMG file.

#### Key Findings
- The mounted DMG contains a self-signed information-stealer (.app bundle) that asks for the user's password, harvests browser/wallet/messaging/keychain data, exfiltrates to two C2 servers, establishes LaunchAgent persistence, and trojanizes Ledger Live and Trezor Suite
- The stealer payload is assessed to belong to the **AMOS (Atomic macOS Stealer)** lineage, specifically the modern **C++ Odyssey variant**, based on the malware's staging directory, persistence module and crypto-wallet trojanization behavior
- The infection chain begins with a fake CAPTCHA page that instructs users to run a malicious command in Terminal, which invisibly mounts a DMG via `hdiutil attach -nobrowse` and executes the payload
- The Mach-O binary is a Universal executable (Intel + ARM64), written in C++, with XOR-encrypted embedded config (8-byte rotating key) and SIMD-decrypted inline strings

#### Payload Capabilities (NNApp.app)
- **Credential phishing** via fake osascript System Preferences dialog, validated with `dscl . -authonly`
- **Browser theft** — 8 Chromium-based browsers (Arc, Brave, Chrome, Edge, Opera, Vivaldi, Yandex, CocCoc) and 5 Firefox-based browsers (LibreWolf, SeaMonkey, Tor Browser, Waterfox, Zen)
- **Crypto wallet theft** — 13 standalone wallets (Electrum, Exodus, Atomic, Bitcoin Core, Binance, TonKeeper, and others) + 201 browser wallet extensions
- **Messaging theft** — Telegram, Discord
- **Additional collection** — Apple Notes, Safari cookies, macOS login keychain, user documents (PDF/TXT/RTF)
- **Exfiltration** via `curl POST` to C2 `/api/reports/upload`
- **Persistence** via LaunchAgent `~/Library/LaunchAgents/com.hlpr.agent.plist`
- **Supply-chain hijack** — trojanizes Ledger Live and Trezor Suite in `/Applications`

#### Indicators of Compromise

**IP Addresses**
- `178.16.52[.]101` (svs-verificationdate[.]beer)
- `196.251.107[.]171` (C2 server)

**Domains**
- `svs-verificationdate[.]beer`
- `fewfwfwfwfwf[.]info` (C2)

**SHA-256 Hashes**
| File | Hash |
|---|---|
| s.01M0td.dmg | `25b6fc4f9c54a28ba7bfc4dfeafb62c99b59ea6f0d17679219b876b321965095` |
| NNApp.app (bundle) | `067ad6221b2224d5cdb64e51c5516132d820cf4d7edf9ec170643943e79c04b7` |
| Mach-O x64 | `d6f479736ba55d3c4e895c4940d035cf772f3192fb8dc496f09a801aed16d970` |
| Mach-O ARM64 | `833008c03d40422192051584d829d730497108bef31751cceb0cc043dd96bbfb` |

**Host Artifacts**
- `~/.hlpr/` — staging directory
- `~/.hlpr/User Name.txt`
- `~/.hlpr/System Information.txt`
- `~/Library/LaunchAgents/com.hlpr.agent.plist` — persistence

**URLs**
- `hxxp[:]//svs-verificationdate[.]beer/f0038a5f46720da5982b6984ceef10cf99359432e102b12a0b0657498d36f670`
- `hxxps[:]//fewfwfwfwfwf[.]info`
- `hxxp[:]//196.251.107[.]171:3000`

---

## License

© Bhargav Rathod. All rights reserved.
