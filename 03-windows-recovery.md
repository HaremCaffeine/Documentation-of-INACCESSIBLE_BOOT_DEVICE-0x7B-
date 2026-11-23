# 03. Windows Recovery Environment Investigation

## Overview

After confirming that the internal NVMe SSD was detected in BIOS, the next step was to investigate the boot failure using the **Windows Recovery Environment (WinRE)**.

WinRE provides built-in troubleshooting tools that help diagnose and repair Windows startup problems without entering the normal desktop.

## Recovery Environment Access

A bootable Windows 11 USB drive was used to access the recovery environment.

The available recovery options included:

- Continue
- Use a device
- Troubleshoot
- Turn off your PC

The Troubleshoot section provided access to additional recovery and diagnostic tools.

## Initial Troubleshooting

The first attempt involved selecting:

**Troubleshoot → Advanced options → Uninstall Updates → Uninstall latest quality update**

However, uninstalling the latest quality update did not resolve the boot failure. The system returned to the recovery environment.

## Command Prompt Investigation

Command Prompt was opened through:

**Troubleshoot → Advanced options → Command Prompt**

DiskPart was then used to investigate available storage devices.

Commands executed:

```cmd
diskpart
list disk
list volume
```

Initially, the internal NVMe SSD was not visible through DiskPart.

This was an important observation because the SSD had already been detected in BIOS.

## Initial Findings

The investigation revealed:

1. Windows could not boot normally.
2. Automatic Repair did not resolve the problem.
3. Uninstalling the latest quality update was unsuccessful.
4. The internal SSD was detected in BIOS.
5. The internal SSD was initially unavailable through DiskPart in WinRE.

These findings suggested a possible storage-controller driver issue involving Intel RST/VMD.

## Next Investigation

The next stage focused on identifying and loading the required Intel VMD storage driver into Windows Recovery Environment.

**Status:** WinRE accessed successfully. Initial disk detection investigation completed.
