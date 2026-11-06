# Lessons Learned

Problems I ran into while building and hardening this lab, and how I solved them.

## Building the VM (Hyper-V)

### VM wouldn't start: "Unable to allocate 4096 MB of RAM" (0x800705AA)
**Cause:** The host didn't have 4 GB of free memory when the VM started.
**Fix:** Closed other applications to free memory before starting the VM.
**Takeaway:** Plan host memory for both the host OS and every VM it runs.

### "No operating system was loaded" / "The boot loader failed"
**Cause:** Missed the 5-second "Press any key to boot from CD or DVD" prompt, so the VM skipped the installer.
**Fix:** Clicked inside the VM window to give it keyboard focus and pressed a key immediately after starting the VM.

### Hyper-V Manager couldn't connect to the local computer
**Cause:** The Hyper-V Virtual Machine Management service wasn't running.
**Fix:** Started the service and restarted the host.

### BitLocker wouldn't turn on with installation media attached
**Cause:** The Windows ISO was still mounted in the VM's virtual DVD drive.
**Fix:** Removed the ISO (DVD Drive → Media: None), restarted, and ran BitLocker setup again.
**Takeaway:** Always remove installation media after setup.

## Hardening the VM

### Local Group Policy "User Configuration" applies to administrators too
**Cause:** Settings made in `gpedit.msc` under User Configuration apply to *every* account on the machine.
**Fix:** Used a Multiple Local Group Policy Object (MMC → Group Policy Object Editor → Browse → Users → Non-Administrators) so restrictions only apply to standard users.

### `Set-MpPreference -ScanScheduleDay 0` doesn't mean Sunday
**Cause:** `0` = every day; `1` = Sunday. The default scan type is also a quick scan, not a full scan.
**Fix:** `Set-MpPreference -ScanParameters FullScan -ScanScheduleDay Sunday -ScanScheduleTime 01:00:00`

<!-- Add new lessons below as you work through each part -->
