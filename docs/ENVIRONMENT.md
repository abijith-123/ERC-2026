# Environment — 2026-09-07

Read-only measurements: sources/windows-diagnostics.json.

| Item | Observed |
|---|---|
| Host | Surface Laptop 4 |
| OS | Windows 11 Pro 10.0.26200, 64-bit |
| CPU | i7-1185G7 @ 3 GHz, 64-bit address width |
| RAM | 34,194,063,360 bytes (~31.85 GiB, 32 GB class) |
| GPU | Intel Iris Xe, driver 32.0.101.6737 |
| Disk | SK hynix BC711 NVMe, 512,110,190,592 bytes, GPT |
| C: free | 395,349,114,880 bytes (~368.2 GiB) |
| Largest unallocated extent | 2 MiB |
| Partitions | 100 MiB System; 16 MiB Reserved; C: Basic; ~948 MiB Recovery |
| HypervisorPresent | true |
| VirtualizationFirmwareEnabled / VMMonitorModeExtensions | false / false |

A running hypervisor makes the false CPU virtualization fields inconclusive; do not infer firmware virtualization is disabled. Direct setting verification remains unresolved. Native Linux Docker does not require a VM host layer.

No Linux partition was detected in the internal disk layout. Ubuntu is not running; an external installation cannot be excluded. Firmware boot enumeration and BitLocker status commands were denied. Encryption is UNKNOWN, not off. No disk, boot, firmware or encryption settings changed.

Workspace initially empty; no workspace AGENTS.md found. Git absent from PATH and common install locations; project-local portable MinGit prepared for local audit version control. Target is native Ubuntu 22.04.5 AMD64 with Xorg and official Docker. Linux input/network/graphics and simulator performance remain untested.
