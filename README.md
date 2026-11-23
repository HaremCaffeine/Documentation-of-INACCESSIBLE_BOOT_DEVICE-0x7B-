# Documentation-of-INACCESSIBLE_BOOT_DEVICE-0x7B- ASUS VivoBook X1500EA 

**Documented by Harem Caffeine**

Cybersecurity • Privacy • Technology

---

A practical technical case study documenting
Windows 11 boot recovery and Intel RST/VMD
storage-driver investigation.
This project documents the troubleshooting and recovery of a Windows 11 boot failure on an ASUS VivoBook X1500EA. The system displayed the INACCESSIBLE_BOOT_DEVICE (0x7B) stop code and repeatedly entered Windows Automatic Repair instead of starting normally.

## Overview

This repository documents the troubleshooting process used to recover an ASUS VivoBook X1500EA that encountered a Windows Blue Screen of Death (BSOD).

**Original error:**

`INACCESSIBLE_BOOT_DEVICE (0x7B)`

The laptop repeatedly entered Windows Automatic Repair and Recovery environments without successfully booting into Windows.

The investigation identified an Intel Rapid Storage Technology (IRST) / VMD storage-driver issue as a possible cause.

## Laptop Specifications

| Component | Details |
|---|---|
| Manufacturer | ASUS |
| Model | VivoBook X1500EA |
| Processor | Intel Core i3-1115G4 |
| RAM | 8 GB |
| Storage | Micron 2400 512GB NVMe SSD |
| Storage Controller | Intel RST / VMD |
| BIOS Version | 316 |
| Operating System | Windows 11 |

## Symptoms

- Windows repeatedly displayed a Blue Screen of Death.
- Stop code: `INACCESSIBLE_BOOT_DEVICE`.
- Automatic Repair failed to resolve the problem.
- Uninstall Latest Quality Update did not resolve the boot loop.
- Windows Recovery initially could not detect the internal SSD.
- BIOS detected the internal SSD.

## Root Cause Investigation

The internal SSD became visible in Windows Recovery Environment after loading the Intel RST VMD storage driver.

This indicated that the recovery environment needed the appropriate storage driver to access the SSD.

The precise original cause of the boot failure was not conclusively established.

## Driver Information

**Intel Rapid Storage Technology (IRST)**

- Version: 18.6.1.1016
- Driver file: `iaStorVD.inf`
- Provider: Intel Corporation
- Driver date: 23 July 2021

Official ASUS support:

https://www.asus.com/supportonly/x1500ea/helpdesk_download/

## Recovery Procedure

### Step 1: Prepare the USB drive

- Download the Intel RST driver from the ASUS support website.
- Extract the driver package.
- Copy the extracted driver files to a USB flash drive.

### Step 2: Access Windows Recovery Environment

Navigate to:

Troubleshoot → Advanced Options → Command Prompt

### Step 3: Identify the USB drive

Use:

```cmd
diskpart
list volume
exit
```

Identify the USB drive letter.

### Step 4: Locate the Intel driver

Search for the INF file:

```cmd
dir C:\*.inf /s
```

The driver was located at:

```text
C:\20261122212617\iaStorVD.inf
```

Note: Drive letters and folder names can differ between systems.

### Step 5: Load the Intel RST driver

Execute:

```cmd
drvload "C:\20261122212617\iaStorVD.inf"
```

The recovery environment reported successful driver loading.

### Step 6: Verify SSD detection

Execute:

```cmd
diskpart
rescan
list disk
```

The internal Micron SSD appeared as an approximately 476 GB disk.

### Step 7: Verify partitions

Execute:

```cmd
list volume
```

The Windows partition, EFI System Partition and Recovery partition became visible.

### Step 8: Restart Windows

Exit Command Prompt and return to the Windows Recovery menu.

Select:

**Continue → Exit and continue to Windows 11**

Windows successfully reached the lock screen and booted into the existing installation.

## Post-Recovery Verification

The following checks were performed:

- Windows 11 successfully booted.
- Internal SSD was detected.
- Intel RST VMD controllers appeared in Device Manager.
- Intel RST driver version 18.6.1.1016 was identified.
- PowerShell reported the Micron SSD health status as Healthy and operational status as OK.

## Important Notes

- Do not format the SSD during troubleshooting.
- Do not delete existing partitions unnecessarily.
- Do not randomly change Intel VMD/RST settings in BIOS.
- Use the correct storage driver for the laptop model.
- Always back up important files before performing recovery operations.

## Final Result

**Windows 11 successfully booted on the ASUS VivoBook X1500EA without performing a clean installation.**

This case study demonstrates how loading the appropriate Intel RST storage driver into Windows Recovery Environment can restore SSD visibility and help troubleshoot boot failures.

## Disclaimer

This documentation describes one troubleshooting experience. Results may vary depending on the BIOS configuration, Windows version, SSD, storage controller and driver compatibility.

Always verify drive letters and back up important data before attempting recovery operations.

---

**Project status:** Initial boot recovery successful. Long-term stability verification remains necessary.
