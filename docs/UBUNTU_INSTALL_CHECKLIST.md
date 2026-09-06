# Safe native Ubuntu 22.04 installation checklist

Prepared 2026-09-07. These are manual instructions. No disk/boot/encryption changes have been made by the agent.

## Before ANY partition changes

1. Back up important files to a separate device, including this entire ERC folder. Open several backed-up files. Ensure OneDrive files are downloaded, not merely cloud placeholders.
2. Open Windows Manage BitLocker. If enabled, save the recovery key somewhere accessible without this laptop. Do not put the key in this project/chat. The agent's status query was denied; encryption status is UNKNOWN.
3. Verify sufficient free AND unallocated space. C: has ~368 GiB free internally, but Disk 0 has only 2 MiB unallocated.
4. Create an Ubuntu installation USB using a spare USB of at least 16 GB whose contents can be erased.
5. Verify UEFI/USB boot settings; retain original settings and Windows Boot Manager. Try Secure Boot enabled first.
6. Avoid deleting/formatting Windows, EFI System, Microsoft Reserved and Recovery partitions. NEVER choose Erase disk and install Ubuntu on the internal drive.

Keep the charger connected. Stop if disk identities or the proposed changes do not match expectations.

## 1. Prepare USB

Download **ubuntu-22.04.5-desktop-amd64.iso** and SHA256SUMS from [Canonical's 22.04 directory](https://releases.ubuntu.com/22.04/). AMD64 is correct for this Intel CPU. Do not select ARM, WSL or Server.

Verify the downloaded ISO in PowerShell, replacing the example with its actual path:

```powershell
Get-FileHash -Algorithm SHA256 -LiteralPath 'C:\path\to\ubuntu-22.04.5-desktop-amd64.iso'
```

Compare the full hash against the matching filename in SHA256SUMS. Do not use a mismatching image.

Follow [Canonical's Rufus Windows USB guide](https://ubuntu.com/tutorials/create-a-usb-stick-on-windows). Download Rufus using its official link. Select the spare USB by model/capacity, select the ISO, choose GPT/UEFI (non-CSM) for this GPT machine, retain filesystem settings appropriate to the image and start writing. Confirm erasure ONLY of that spare USB. The agent has not downloaded the ISO or erased a USB.

## 2. Try Ubuntu before resizing

Windows 11: Settings > System > Recovery > Advanced startup > Restart now > Use a device > USB Storage (or named UEFI USB). [Microsoft Surface USB instructions](https://support.microsoft.com/en-us/surface/drivers-firmware/boot-surface-from-a-usb-device).

If absent, enter Troubleshoot > Advanced options > UEFI Firmware Settings and inspect Boot configuration/USB boot. Preserve Windows Boot Manager. If Secure Boot rejects the image, stop to diagnose the exact message before changing security settings.

Choose Try Ubuntu. Test keyboard, touchpad, Wi-Fi and display; have a USB keyboard/mouse available if needed. In Terminal:

```bash
uname -m
lsb_release -a
lsblk -o NAME,SIZE,FSTYPE,MOUNTPOINTS
test -d /sys/firmware/efi && echo 'Booted in UEFI mode'
```

Expected: x86_64, Ubuntu 22.04, UEFI mode, internal ~512 GB disk visible. This live session is a compatibility test, not the installed development OS. If essential input/storage/network fails, report the exact problem before installing.

## 3. Prepare space manually in Windows

Reboot Windows. Verify backup and recovery key. Disable Fast Startup through Control Panel > Power Options > Choose what the power buttons do > Change settings that are currently unavailable. Fully shut down Windows before accessing it from Linux.

If BitLocker is enabled and Ubuntu refuses installation alongside Windows, consult [Canonical's BitLocker guidance](https://ubuntu.com/tutorials/install-ubuntu-desktop). Turning BitLocker off decrypts the drive; suspending protection is different. Make that decision yourself after saving the key and wait for decryption if chosen. No automatic decryption is authorized. A separate external SSD with its own EFI partition is an alternative native installation, but requires a disk-specific plan so its boot files do not inadvertently go on the internal disk.

Win+X > Disk Management. Confirm Disk 0 is the SK hynix BC711 ~512 GB drive. Right-click C: > Shrink Volume. Suggested allocation: **150 GiB**, entered as **153600 MB**. This is our engineering recommendation, not a competition requirement. If Windows cannot shrink sufficiently, stop and reassess rather than deleting Recovery or forcing an offline resize. Leave the new space Unallocated; do not format it as NTFS.

## 4. Install alongside Windows

Boot the USB in UEFI mode and select Install Ubuntu. Choose language, keyboard/network and normal desktop installation. The 22.04 installer differs visually from current Canonical tutorials.

Prefer Install Ubuntu alongside Windows Boot Manager if available, inspecting its proposed space allocation. If only Erase disk is offered, do not choose it.

For Something else/manual partitioning, proceed only if comfortable identifying partitions: create an ext4 partition mounted at `/` ONLY in the newly unallocated space. Preserve all existing partitions. Mount the existing EFI System Partition at `/boot/efi` WITHOUT formatting it. Do not create a new partition table. Installing dual boot adds Ubuntu boot files. If the EFI partition is too small or any identity is unclear, stop instead of resizing/deleting it.

Before Install Now, inspect the write-to-disk summary: formatting must affect only the new Ubuntu root partition. C:, EFI, Reserved and Recovery must not be formatted. Cancel unexpected deletions/format actions.

Complete username/timezone setup. Restart and remove USB when instructed. Verify installed Ubuntu and Windows both boot. Do not upgrade Ubuntu to another release. At Ubuntu login, select Ubuntu on Xorg using the session gear; the official simulator expects X11.

## 5. Resume

Restore the backed-up ERC folder including PROJECT_STATUS.md, docs and .git onto Ubuntu's native filesystem, preferably ~/erc2026/progress. Do not develop on NTFS/OneDrive. Official/reference repositories can be cloned fresh on Linux; Windows checkouts are only research snapshots.

Relaunch the coding session under installed Ubuntu and open the restored folder. The next agent will run diagnostics, recheck official releases/issues, install required Docker prerequisites and use the official scripts. Do not manually install ROS on the host.

**Send back: Ubuntu 22.04 is running, plus the restored PROJECT_STATUS.md path.** If installation is blocked, send the exact screen/error instead of continuing past it.
