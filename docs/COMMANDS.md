# Command log — Phase 0

All commands ran from C:\Users\Surface Laptop\OneDrive\Desktop\ERC unless noted. Read-only diagnostics; no privileged storage/boot changes.

## Successful

- Get-Content -LiteralPath <attachment>/pasted-text.txt (UTF8 reread for detailed middle sections); saved full request locally in docs/sources/USER_REQUEST.txt.
- Get-CimInstance Win32_OperatingSystem / Win32_Processor / Win32_ComputerSystem / Win32_VideoController.
- Get-Volume; Get-Disk; Get-Partition; converted selected results to docs/sources/windows-diagnostics.json.
- Invoke-WebRequest and Invoke-RestMethod for official README, GitHub all-state issues/comments, releases/tags/main SHA, repository trees, Docker scripts, PDF and reference source. API request headers: User-Agent ERC-Phase0-Audit. Sources saved in docs/sources.
- Get-FileHash docs/sources/official-phase1.pdf -Algorithm SHA256.
- Portable MinGit downloaded from https://github.com/git-for-windows/git/releases/download/v2.55.0.windows.5/MinGit-2.55.0.5-64-bit.zip and Expand-Archive to .tools/mingit. No global PATH changes or system installation.
- & ./.tools/mingit/cmd/git.exe --version (2.55.0.windows.5).
- & ./.tools/mingit/cmd/git.exe init -b feature/erc-phase1-solution.
- & ./.tools/mingit/cmd/git.exe -c core.longpaths=true clone --depth 1 --branch v1.0.3 https://github.com/dfl-rlab/erc_sim_2026.git official/erc_sim_2026.
- & ./.tools/mingit/cmd/git.exe clone --depth 1 https://github.com/SaberFaceLove/erc-competition-2026.git references/SaberFaceLove-erc-competition-2026.

## Failed / limited

- Initial git status: Git not on PATH. After portable Git, pre-init status correctly reported no repository; then initialized empty workspace.
- rg --files -g AGENTS.md: no workspace matches (exit 1).
- Initial mixed PowerShell table output obscured columns; reran selected diagnostics as JSON successfully.
- manage-bde -status C: and bcdedit /enum firmware: access denied. No escalation attempted; manual safety checklist covers these unknowns.
- Guessed official src/erc_bringup/scripts/gripper_clamp.py URL: 404; repository tree located gripper_command_clamp.py, fetched and inspected successfully.
- Search for Git in WindowsApps returned no usable executable.
- One apply_patch batch rejected because it tried delete/add of the same document in one patch; no changes applied by that attempt. Documents subsequently written successfully with PowerShell UTF8 here-strings.

## Next phase commands — NOT run on Windows

After native Ubuntu, revalidate OS and upstream release first:

```bash
uname -a
uname -m
lsb_release -a
free -h
df -h
lscpu
lspci | grep -Ei 'vga|3d|display'
docker --version
docker compose version
git --version
python3 --version
echo "$XDG_SESSION_TYPE"
```

Install only needed Docker/Linux host prerequisites following current official documentation, then from official repository root:

```bash
./docker/up.sh --build
./docker/attach.sh
# Inside container:
colcon build --symlink-install
source install/setup.bash
ros2 launch erc_bringup simulation.launch.py
```

For subsequent terminals use attach.sh only. up.sh stops/removes the existing erc_sim container and rebuilds without cache when --build is passed; do not run it to open another shell. Network required for an uncached build. Do not issue README motion examples until baseline safety conditions and stop command are prepared.

Final checks: nine required documents exist/nonempty; PDF SHA256 matches; official/reference git status clean. Local audit commit uses explicit agent identity Codex <codex@localhost> for this command only because user.name/email were not configured; no global identity changes.
