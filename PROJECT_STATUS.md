# PROJECT STATUS

Updated 2026-09-07. PHASE 0 — review complete; STATUS BLOCKED on manual native Ubuntu installation. No robot code written.

## Completed

- Detected Windows 11 Pro on Surface Laptop 4, i7-1185G7, 32 GB-class RAM, Iris Xe, ~368 GiB free C: but 2 MiB unallocated.
- Saved hardware JSON, original user request, official main README/scripts, eight-page Phase 1 PDF and GitHub issues/comments/releases/tags.
- Reviewed official requirements and separated assumptions/interfaces/decisions/questions in docs/COMPETITION_REQUIREMENTS.md.
- Cloned official latest release v1.0.3 and unofficial reference separately. No reference code reused; license unspecified.
- Prepared docs/UBUNTU_INSTALL_CHECKLIST.md with backups, BitLocker key, manual space preparation, USB/UEFI checks and Windows-preserving dual boot.
- Prepared local audit Git repository using portable MinGit; no remote configured or push.

## Current blockers and important findings

Ubuntu is not running. User explicitly requires stopping on Windows before partition/boot changes. Do not continue simulator installation here. BitLocker/firmware enumeration denied; no Linux partition detected on internal disk, external installations not excluded. Virtualization fields inconclusive because a hypervisor is present.

Official gripper issue #2 remains open; experimental fix updated September 6 has not been treated as released. Nav2/MoveIt are installed but need team configuration. Row numbering direction needs confirmation before implementation. Deadline on RIT page: September 15, 2026.

## Paths / branches

Current audit: C:\Users\Surface Laptop\OneDrive\Desktop\ERC
Audit branch: feature/erc-phase1-solution. Commit: use git log -1 after final milestone commit.
Git executable: .tools/mingit/cmd/git.exe (local portable tool; not committed).
Official: official/erc_sim_2026, detached release v1.0.3 at 0a09806ecbade5edc9f8a148b7c9f439ed761554, read-only baseline.
Official main reviewed separately: 2aa5a4a7d19177e0bb6625ea5f2c37f7b32bd33a.
Reference: references/SaberFaceLove-erc-competition-2026, main; record SHA in sources/repository-checks.txt.
Submission: not created; aurak_erc_solution is provisional future package name.

Linux destination plan: ~/erc2026/progress (this audit); ~/erc2026/official/erc_sim_2026; ~/erc2026/references/SaberFaceLove-erc-competition-2026; ~/erc2026/submission; ~/erc2026/evidence.

## Commands and tests

Worked: PowerShell CIM/storage JSON, HTTP/API retrieval, PDF hash, portable Git and separate clones. Failed: PATH git, non-repository pre-init status, BitLocker/boot access, guessed gripper script URL (corrected). Exact commands/outcomes in docs/COMMANDS.md. Tests in docs/TEST_RESULTS.md. Runtime ROS/Gazebo/control tests NOT RUN.

## Next exact task

USER: follow docs/UBUNTU_INSTALL_CHECKLIST.md to install native Ubuntu 22.04.5 AMD64 safely; preserve Windows. Restore this folder (including docs and .git) onto Linux filesystem and relaunch coding session there. Report Ubuntu 22.04 running and restored PROJECT_STATUS.md path. No need to write source code.

NEXT AGENT: read this file, docs/DECISIONS.md, docs/COMPETITION_REQUIREMENTS.md and local original request if present. Verify installed native Ubuntu 22.04 x86_64, not merely live USB/WSL; inspect CPU/RAM/disk/GPU/Xorg. Recheck official release, main and issue #2 before choosing baseline. Clone clean on Linux. Install needed Docker host prerequisites per current official instructions, run official up.sh --build, attach, colcon build --symlink-install, source and simulation.launch.py. Verify simulator before basic controls; then live interface discovery, then perception scoring. Follow user phases, safety and persistence requirements.

Do not change robot/world/physics, use both arms, invent trial success, push GitHub, or publish without authorization. No disk/boot/encryption changes were made in Phase 0.

## USB preparation update
User approved erasing external D: (32 GB USB, serial 121220160204) and declined backup. Installer download in progress; Rufus signed by Akeo Consulting prepared. No USB write yet. See docs/USB_PREPARATION.md. Internal-disk/boot changes remain outside this authorization.

USB milestone: Ubuntu ISO complete and SHA256 verified. Rufus open, correct D: device observed. Elevated UI ignores automated clicks; user asked to select the prepared ISO. USB write and verification remain pending. Windows partitions unchanged.

USB creation milestone: user completed Rufus write. D: identity rechecked; GPT/FAT32 and Ubuntu 22.04.5 AMD64 boot files verified. Next exact user action: boot USB through Windows Advanced startup > Use a device, then Try Ubuntu for compatibility test. Do not install/resize yet. Session will disconnect on reboot; progress is saved here.
