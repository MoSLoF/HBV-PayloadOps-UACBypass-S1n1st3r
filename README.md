# HBV-PayloadOps-UACBypass-S1n1st3r

UAC bypass and encrypted payload loader for the Hak5 Bash Bunny. Drops an AES-encrypted DLL, decrypts it in memory, and executes via reflection loading.

Currently bypasses Defender and BitDefender.

## How It Works

1. Bash Bunny mounts as USB storage with HID attack mode
2. `payload.txt` launches a hidden PowerShell session pointing to `installer.ps1`
3. `installer.ps1` reads the encrypted DLL from the Bunny's storage
4. DLL is decrypted (AES + XOR), loaded via reflection, and executed in memory

The UAC bypass technique is based on [this research](https://0x00-0x00.github.io/research/2018/10/31/How-to-bypass-UAC-in-newer-Windows-versions.html).

## Prerequisites

- Hak5 Bash Bunny with USB label set to `UPDATE`
- Windows 10+ target
- `chromeUpdater.dll` (encrypted payload) placed in `payloads\<switch_position>\`

## Files

| File | Purpose |
|------|---------|
| `payload.txt` | Bash Bunny attack script (HID + Storage mode) |
| `installer.ps1` | AES decryption and reflective DLL loader |
| `chromeUpdater.dll` | Encrypted DLL payload |

## Usage

1. Copy all files to the appropriate Bash Bunny switch position directory
2. Ensure the Bash Bunny USB volume label is `UPDATE`
3. Insert Bash Bunny into target system
4. Payload auto-executes via HID injection

## Disclaimer

For authorized penetration testing and security research only. Ensure you have explicit written permission before deploying against any system.


---

## HoneyBadger Vanguard

**Part of the [HoneyBadger Vanguard (HBV)](https://ihbv.io) purple team ecosystem.**

Bash Bunny UAC bypass loader — HID+Storage attack, Chrome updater DLL preloading. MITRE T1548.002.

```powershell
$global:Intent = 'Purple'  # Understand offense. Build better defense.
```

| | |
|---|---|
| **Org** | [MoSLoF on GitHub](https://github.com/MoSLoF) |
| **Platform** | HoneyBadger Vanguard 2.0 |
| **Demo Target** | CyberShield 2026 - Little Rock, AR |
| **License** | See LICENSE |

> The difference between a red team tool and a purple team tool is intent.
> -- $global:Intent = 'Purple'
