<img width="860" height="484" alt="02-bios-information" src="https://github.com/user-attachments/assets/bd052f89-7545-4607-87da-24725a7a3327" />
# 02. BIOS Investigation

## Overview

The next step was to investigate whether the laptop's internal storage device was being detected by the BIOS.

Since Windows displayed the `INACCESSIBLE_BOOT_DEVICE (0x7B)` error, checking SSD detection was an important part of identifying the possible cause.

## System Information

| Component | Details |
|---|---|
| Laptop | ASUS VivoBook X1500EA |
| BIOS Version | 316 |
| Storage Device | Micron 2400 512 GB NVMe SSD |
| Storage Interface | NVMe |

## Investigation Steps

1. Restarted the ASUS VivoBook X1500EA.
2. Entered BIOS Setup.
3. Navigated through the available BIOS information and storage-related sections.
4. Checked whether the internal NVMe SSD was detected.
5. Confirmed that the Micron 2400 SSD was visible in BIOS.

## Observation

<badge color="success">SSD detected in BIOS</badge>

The internal Micron 2400 512 GB NVMe SSD was detected successfully by the BIOS.

This observation suggested that the SSD was at least being recognized at the firmware level.

However, BIOS detection alone does not confirm that the SSD, its partitions, or Windows installation are fully healthy.

## Initial Conclusion

The investigation did not immediately indicate a complete SSD detection failure.

The next step was to investigate why Windows Recovery Environment could not initially access the internal storage through DiskPart.

A possible Intel Rapid Storage Technology (RST) or Volume Management Device (VMD) driver issue became an area for further investigation.

## Important Note

No BIOS configuration changes or storage-mode modifications are documented as part of this investigation.

**Result:** Internal SSD detection in BIOS confirmed. Further Windows Recovery Environment investigation required.
