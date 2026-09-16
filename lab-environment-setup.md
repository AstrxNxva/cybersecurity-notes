# Lab Environment: Hardware History & Stock vs Current Setup

## Hardware Upgrade History
| Component | Original (Stock) | Upgraded (Current) |
|---|---|---|
| RAM | 4 GB | 12 GB |
| Storage | 16 GB | 1 TB (128GB SSD + 1TB HDD) |

The original 4GB RAM / 16GB storage configuration would not have been viable
for running virtual machines at all. The RAM and storage upgrades were a
prerequisite for setting up any home lab — without them, even a single Kali VM
would not run.

## Hardware (Current)
| Component | Spec |
|---|---|
| Model | HP Pavilion x360 Convertible 14-ba0xx |
| CPU | Intel Core i3-7100U (2 cores / 4 threads, 2.40GHz) |
| RAM | 12 GB (upgraded from 4 GB) |
| Storage | 128GB SSD (SanDisk SD8SN8U) + 1TB HDD (Seagate ST1000LM035) — upgraded from 16GB total |
| BIOS | Insyde F.22 (UEFI) |

## Stock Configuration (Before)
- **OS:** Windows 10 Home only
- **Boot mode:** UEFI with Secure Boot enabled
- **Disk layout:** Windows fully installed on the 128GB SSD (C:); 1TB HDD used entirely as a single NTFS data drive (D:)
- **Purpose at this stage:** General use, web design/agency work (Webflow)

## Current Configuration (After)
- **OS:** Dual-boot — Windows 10 Home (SSD) + Ubuntu 26.04.1 LTS (HDD)
- **Boot mode:** Secure Boot disabled to allow Ubuntu installation; GRUB bootloader manages OS selection at startup
- **Disk layout changes:**
  - SSD (sda): untouched, still runs Windows fully
  - HDD (sdb): shrunk to free ~104GB — sdb3 (103.73GB, Ext4, mounted at `/`) for Ubuntu root, sdb4 (1.13GB, FAT32, mounted at `/boot/efi`) for Ubuntu's boot partition
  - Remaining ~880GB of HDD kept as NTFS data storage, unaffected
- **Tools installed for security learning:**
  - Wireshark (network traffic analysis)
  - VirtualBox (virtualization for home lab VMs)
  - Kali Linux (attacker VM)
  - Metasploitable2 (deliberately vulnerable target VM)
- **Network isolation:** Kali and Metasploitable2 configured on a Host-only Adapter, isolated from the main network

## Key Trade-off Identified
Ubuntu runs on the mechanical HDD rather than the SSD, since the SSD was already near capacity with Windows. This means:
- VM boot times and disk-heavy operations are noticeably slower than they would be on SSD
- Mitigation applied: VM disk files pointed at available SSD space where possible to reduce the impact

## Why This Setup Works for a Beginner Home Lab
Running Kali and Metasploitable side by side, isolated from the real network, is sufficient for practicing web enumeration (e.g. DirBuster) and basic exploitation techniques without any real-world risk, and without requiring new hardware beyond the RAM/storage upgrades already made.

## Future Upgrade Path (If Scaling Up)
If moving into more demanding labs (e.g. Active Directory environments, multiple simultaneous VMs), the recommended upgrade path would be:
- Quad-core+ CPU (i5/Ryzen 5 or better)
- 16–32GB RAM
- NVMe SSD, 512GB+, as primary drive for both OS and VM storage
