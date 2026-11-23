# 05. Internal SSD Detection and Partition Investigation

## Overview

After successfully loading the Intel VMD storage driver into Windows Recovery Environment (WinRE), the next step was to verify whether the internal NVMe SSD had become accessible.

DiskPart was used to rescan the storage devices and inspect the available disks and partitions.

## Commands Executed

The following commands were entered in Command Prompt:

```cmd
diskpart
rescan
list disk
list volume
```

## Disk Detection Result

After the driver was loaded, DiskPart successfully detected the internal Micron 2400 512 GB NVMe SSD.

The internal drive appeared with approximately 476 GB of usable capacity.

<badge color="success">Internal SSD detected</badge>

## Volume Information

The following volumes were identified during the investigation:

| Volume | Approximate Size | File System | Purpose |
|---|---:|---|---|
| USB Drive (C:) | 32 GB | FAT32 | Windows recovery USB |
| Windows Partition (D:) | 475 GB | NTFS | Installed Windows and data |
| EFI Partition | 200 MB | FAT32 | UEFI boot files |
| Recovery Partition | 923 MB | NTFS | Windows recovery environment |

*Drive letters are specific to the recovery environment and may differ during normal Windows operation.*

## Important Observations

1. The internal NVMe SSD became visible after loading `iaStorVD.inf`.
2. DiskPart successfully rescanned the available storage devices.
3. The Windows partition was visible as an NTFS volume.
4. The EFI System Partition was also detected.
5. The Recovery Partition was present.

These observations confirmed that WinRE could access the internal SSD after loading the storage driver.

## Technical Significance

The successful detection of the SSD and its partitions narrowed the investigation toward a possible storage-controller driver accessibility issue.

However, partition visibility alone does not prove that the Windows installation or boot configuration is completely healthy.

No partition formatting, deletion, or resizing was performed as part of this documented investigation.

## Result

The internal Micron 2400 NVMe SSD and its important partitions were successfully detected through DiskPart.

**Next Step:** Exit Windows Recovery Environment and attempt a normal Windows 11 startup.<img width="1155" height="740" alt="Screenshot 2026-11-23 072524" src="https://github.com/user-attachments/assets/39e3ee6c-7438-45b2-b326-5c927f6541ed" />
