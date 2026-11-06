# Windows 11 Endpoint Hardening Lab

Hardening a Windows 11 Pro virtual machine the way an IT team would before rolling it out to a company: local security baselines, restricted standard users, UAC hardening, scheduled maintenance and antivirus scans, and verification with event logs and PowerShell.

> 🚧 **Status:** In progress. I'm updating this repo as I complete each part.

## Lab Environment

| Component | Configuration |
|---|---|
| Hypervisor | Microsoft Hyper-V |
| Guest OS | Windows 11 Pro (Generation 2 VM, UEFI) |
| Security hardware | Secure Boot + virtual TPM 2.0, BitLocker enabled |
| Resources | 2 vCPU, 4 GB RAM, 64 GB system disk + 10 GB data disk |
| Accounts | Local administrator + local standard users (no Microsoft account) |

## Objectives

| # | Area | What I configured | Status |
|---|---|---|---|
| A | Storage | Second virtual disk (D:) for redirected user data | ⬜ |
| B | Least privilege | Standard user account with no admin rights | ⬜ |
| C | Password & lockout policy | 12-character minimum, complexity, 90-day max age, history of 10, lockout after 5 attempts | ⬜ |
| D | User restrictions | Control Panel, Settings and Command Prompt blocked for non-administrators | ⬜ |
| E | UAC hardening | Admin Approval Mode, auto-deny elevation for standard users | ⬜ |
| F | Maintenance automation | Daily disk cleanup task + weekly Microsoft Defender full scan | ⬜ |
| G | Verification | Event Viewer + PowerShell reports confirming each setting | ⬜ |

## Skills Demonstrated

- Windows 11 local security policy (`secpol.msc`) and Local Group Policy (`gpedit.msc`)
- Scoping policies to non-administrators with Multiple Local Group Policy Objects (MLGPO)
- User Account Control (UAC) hardening and least-privilege design
- Task Scheduler and Microsoft Defender configuration with PowerShell
- Verifying configuration with Event Viewer, `secedit`, and `Get-WinEvent`

## Repository Structure

```
├── README.md            Project overview (this file)
├── LESSONS-LEARNED.md   Problems I ran into and how I solved them
├── scripts/             PowerShell scripts to apply and verify each setting
└── screenshots/         Evidence for each part
```

## Why This Matters

Most of these settings would be deployed to a company's laptops with Microsoft Intune or Group Policy. Configuring them by hand on one machine first shows exactly what each setting does, how it affects users, and how to prove it's working before it reaches production.

---
*This is a personal lab environment. No production systems or real user data were used.*
