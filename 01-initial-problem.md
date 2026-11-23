<img width="1920" height="1080" alt="01-blue-screen" src="https://github.com/user-attachments/assets/28b40a69-3167-458a-ad38-cf4b56bffb68" />
# 01. Initial Problem

## Overview

This document describes the initial Windows 11 boot failure encountered on an **ASUS VivoBook X1500EA**.

The laptop failed to start Windows normally and repeatedly entered the Windows Automatic Repair environment.

## System Specifications

| Component | Details |
|---|---|
| Laptop | ASUS VivoBook X1500EA |
| Processor | Intel Core i3-1115G4 (11th Gen) |
| RAM | 8 GB |
| Storage | Micron 2400 512 GB NVMe SSD |
| Operating System | Windows 11 |
| BIOS Version | 316 |

## Problem Description

The issue occurred after an interrupted Windows update situation. The laptop entered a recovery loop instead of booting into the operating system.

The displayed stop code was:

`INACCESSIBLE_BOOT_DEVICE (0x7B)`

This error indicates that Windows cannot access the system boot device during startup.

## Initial Symptoms

- Windows failed to boot normally.
- Automatic Repair repeatedly appeared.
- The system entered the Windows Recovery Environment.
- Uninstalling the latest quality update did not resolve the issue.
- The internal SSD was detected in BIOS.
- The internal SSD was initially not visible through DiskPart in WinRE.

## Initial Observations

Since BIOS detected the NVMe SSD, complete storage-device detection failure was not immediately indicated.

However, the inability of WinRE to access the internal SSD suggested a possible storage-controller or Intel RST/VMD driver compatibility issue.

Further investigation was required before identifying the cause.

## Objective

The primary objective was to restore normal Windows startup without reinstalling Windows or unnecessarily formatting the SSD.

The investigation focused on:

1. Examining BIOS storage detection.
2. Accessing Windows Recovery Environment.
3. Investigating disk visibility through DiskPart.
4. Checking Intel RST/VMD storage drivers.
5. Restoring access to the internal SSD.

**Status:** Initial problem identified. Root cause investigation continued in the next stage.
