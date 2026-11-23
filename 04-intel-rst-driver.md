<img width="700" height="640" alt="04-intel-rst-driver" src="https://github.com/user-attachments/assets/a6d4d7b5-9cf2-49b6-a93d-db3e81ff0888" />
# 04. Intel RST/VMD Driver Investigation

## Overview

During the Windows Recovery Environment investigation, the internal Micron 2400 NVMe SSD was not initially visible through DiskPart.

Since the SSD was detected in BIOS, the next step was to investigate whether WinRE needed an additional storage-controller driver to access it.

The investigation focused on **Intel Rapid Storage Technology (RST)** and **Volume Management Device (VMD)**.

## Driver Information

| Property | Details |
|---|---|
| Driver Provider | Intel Corporation |
| Driver File | `iaStorVD.inf` |
| Driver Version | 18.6.1.1016 |
| Driver Date | 23 July 2021 |
| Controller | Intel RST VMD Controller |

## Driver Location

The required driver was extracted onto the bootable Windows USB drive.

The driver file was located at:

```text
C:\20261122212617\iaStorVD.inf
```

In this recovery environment, `C:` represented the USB drive.

## Loading the Driver

The following command was executed in Command Prompt:

```cmd
drvload "C:\20261122212617\iaStorVD.inf"
```

The command successfully loaded the driver into the Windows Recovery Environment.

<badge color="success">Driver loaded successfully</badge>

## Disk Detection Verification

After loading the driver, DiskPart was opened again:

```cmd
diskpart
rescan
list disk
list volume
```

The internal Micron 2400 NVMe SSD became visible.

This was an important breakthrough because the recovery environment could now access the internal storage.

## Important Technical Note

The `drvload` command loads a driver temporarily into the current Windows PE/Recovery Environment session.

It does not automatically install or inject that driver into the offline Windows installation.

Therefore, this procedure confirmed improved storage visibility in WinRE, not a permanent driver repair.

## Result

The Intel VMD driver loaded successfully, and the internal SSD became accessible through DiskPart.

**Next Step:** Inspect the detected disk and partitions before attempting to boot Windows again.<img width="1165" height="785" alt="Screenshot 2026-11-23 072258" src="https://github.com/user-attachments/assets/06442e58-bb33-4bf2-86a1-7ee90abac3e2" />
