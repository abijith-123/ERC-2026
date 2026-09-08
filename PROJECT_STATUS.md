# PROJECT STATUS

Updated 2026-09-08. Current phase: Windows-compatible vision and alignment prototypes.
STATUS: PASS for offline tests; full autonomous mission INCOMPLETE; ROS/Gazebo integration NOT RUN.

## Current authorization

User explicitly paused USB/Ubuntu work and approved beginning Windows-compatible
coding ("Leave the USB for later", followed by "Do Do"). This supersedes the old
Windows no-coding checkpoint. Do not resume OS installation, reboot, disk changes,
WSL setup or USB writing without new direction. No GitHub push authorized.

## Completed

- Phase 0: hardware measured, official rules/README/releases/issues reviewed and
  saved. Intel Surface Laptop 4, Windows 11 Pro, 32 GB-class RAM, Iris Xe.
- Ubuntu 22.04.5 USB was created by user, GPT/FAT32 and EFI/kernel/initrd files
  verified; actual Ubuntu boot failed to progress beyond normal Windows boot.
  USB task now paused. No Windows partitions/encryption/boot settings changed.
- Created independent submission Git repository with aurak_erc_solution package.
- Strict request validation; validated JSON-form YAML config; deterministic mission
  states with timeouts/retry bounds/delivery gate; sensor watchdog/contact counting;
  observed-label/row geometry; annotated PNG writer and validated JSON metrics.
- solution.launch.py exposes the two required arguments, no simulator launch.
  Current ROS adapter is READ-ONLY CAMERA PREFLIGHT, untested in ROS. No scoring or
  motion publishers; no actual digit/book/bin detector, navigation or arm control.
- Added trial procedure, video checklist, state integration contract, architecture
  diagram and report outline explicitly stating zero simulation trials.

## Verification

23 offline tests PASS in Windows Python 3.12.14, including all 20 requests and all
120 marker permutations, timeout/failure/retry cases, synthetic PNGs in temporary
folders and metrics integrity. Initial test path mismatch from Windows short/long
path alias fixed by resolving the test root. Re-run passed.

Wheel build PASS; wheel contains launch/config/package.xml/ament marker. CLI valid
input accepted and invalid input rejected from isolated temp cwd with source path
removed. Fresh local submission clone also passed 23 tests. Python 3.10 syntax
checked, not actual Humble/Python 3.10 execution. colcon/ROS/Gazebo NOT RUN.
No live trial metrics or competition evidence images exist. See docs/TEST_RESULTS.md.

## Repositories and tools

Audit root: C:\Users\Surface Laptop\OneDrive\Desktop\ERC
Submission (SEPARATE Git repo): C:\Users\Surface Laptop\OneDrive\Desktop\ERC\submission
Both branches: feature/erc-phase1-solution.
Submission implementation commit: a7dfe26 (provisional vision and feedback alignment policies).
Audit ignores /submission/ intentionally; back up BOTH repositories including .git.
Submission has no remote and no push. Audit commit: use git log -1.
Official baseline: official/erc_sim_2026 at v1.0.3 / 0a09806ecbade5edc9f8a148b7c9f439ed761554.
Official main inspected September 7: 2aa5a4a7d19177e0bb6625ea5f2c37f7b32bd33a.
Reference: references/SaberFaceLove-erc-competition-2026 at 897f5b1f751626b24f8b8edde1bc4bc9fdf08f9c; no code reused.
Validation clone: .tools/submission-validation-20260908 (disposable, ignored).
Git executable: .tools/mingit/cmd/git.exe.
Python: C:\Users\Surface Laptop\.cache\codex-runtimes\codex-primary-runtime\dependencies\python\python.exe.
Bundled Pillow available; pytest/PyYAML absent. Tests use unittest. Config uses JSON subset of YAML.

## Next exact engineering task

Read submission/README.md and submission/docs/STATE_POLICY.md. Do not confuse pure
geometry helpers with a detector or tested policy with robot behaviour. At next
simulator opportunity: recheck official release/issues, verify native Ubuntu/X11,
start unchanged official Docker, colcon build/test and run camera preflight against
actual ROS topics. Verify basic controls before motion implementation. Capture live
randomized shelf images and implement/test digit and book detectors before grasping.
User may direct further Windows development; any such work must retain explicit
untested status for ROS/control integration and cannot claim competition points.

## Remaining blockers and unresolved matters

Native Ubuntu/official simulator not running. ROS interfaces, QoS/TF/controllers,
MoveIt/Nav2 setup and gripper behaviour unverified. Historical: official #2 grasp issue was
open September 7 with an experimental September 6 patch, not established baseline.
Row numbering direction still unresolved; helper requires explicit top-row number.
Maintainer contact is placeholder; proprietary license is provisional, no public
license chosen. Deadline last verified on RIT page: September 15, 2026.

Commands/results: docs/COMMANDS.md, docs/TEST_RESULTS.md. Evidence logs are in
sources/windows-foundation-tests.txt and sources/windows-clean-clone-tests.txt.

## Latest milestone — vision prototypes

Added independent OpenCV digit candidates, scoped HSV book-color candidates,
red-bin shape/metric-size proposals, registered-depth unprojection, consecutive
frame stability, endian/padding-aware ROS image decoding and bounded feedback
alignment policy. These are NOT yet wired to ROS scoring/motion. ROS entry remains
read-only preflight. Automatic header/full-column geometry, live calibration,
TF, planners and all manipulation/delivery integration remain pending.

37 tests PASS in current tree and fresh local clone; wheel build/isolated CLI PASS.
Logs: docs/sources/windows-vision-tests.txt and windows-vision-clean-clone-tests.txt.
Development probe on flat official textures: 1–4 accepted correctly, 5 rejected
because similarity gap from 3 was below threshold. Not held-out data or live
accuracy; improving prototype stroke variants used these assets during development.
No assets copied into submission, no fake competition evidence generated.

OpenCV 4.10.0.84 installed locally in .tools/python-packages with --no-deps;
bundled NumPy/Pillow used. Set PYTHONPATH to that directory for current Windows
tests. Submission README documents standard venv installation via offline-vision
extra; ROS package declares distro python3-opencv/python3-numpy dependencies.

UPSTREAM UPDATE: official collaborator confirmed September 8 that gripper fix
merged to main. Main SHA 93554d4f9335b2ee3acb49c6b332611f6ad2a964; latest release
still v1.0.3. Saved docs/sources/official-main-20260908.json. Local official clone
remains unchanged at v1.0.3. Next simulator setup must recheck and consider the
organizer-approved main fix, not assume the older release includes it.

NEXT: actual official simulator runtime and live images are needed to calibrate,
integrate and verify the mission. scripts/capture_interfaces.py is prepared for
read-only inventory inside the official container. USB/native OS work remains
paused; do not treat broader coding request as permission for disk/boot changes.

USB setup resumed at user request: same device D:, serial 121220160204, Ubuntu 22.04.5 boot files reverified. Windows recovery-status query requires elevation (reagentc error 5). Recovery settings opened for manual Advanced startup. Do not alter partitions or install before live compatibility checks and backup/BitLocker prerequisites.

## ACTIVE: WSL2 setup
User explicitly authorized WSL2. Initial wsl --status/list/version say not installed; unprivileged install failed. Elevated Windows PowerShell installer started for wsl --install -d Ubuntu-22.04 --no-launch. Logs/result at .tools/wsl/install.log and result.json. Check these before retrying. No distro success claimed yet; reboot may be needed.

Installer completed successfully (exit 0, 2026-09-08 22:05 +04). WSL version
2.7.13.0, kernel 6.18.33.2-2 and WSLg 1.0.73.2 verified. VirtualMachinePlatform
installation explicitly requires a Windows reboot. `wsl --list --verbose` confirms
no distributions installed yet. NEXT: user saves work and performs a normal
Windows Restart; then verify WSL and install Ubuntu-22.04 with --no-launch.
Do not repeat the completed WSL platform installer or use USB boot for this step.

## WSL2 and Ubuntu installed — 2026-09-08
Windows reboot verified (22:08:47 +04). Automatic distro downloads stalled with
a zero-byte temporary image; cancelled both before a direct IPv4 Canonical download.
Image ubuntu-22.04.5-wsl-amd64.wsl (360684292 bytes) SHA256
4499c4fe257f2fc83145b429ce211a0a43fd590e70d6261ede616210947d9f8f matched
Microsoft/WSL distributions/DistributionInfo.json. Installed with --from-file,
--name Ubuntu-22.04 and --no-launch. Ubuntu 22.04.5 starts successfully with kernel
6.18.33.2-microsoft-standard-WSL2; distro list confirms version 2. systemd PID 1,
WSLg socket and /dev/dxg exist; /dev/dri absent. Graphics not yet tested.
Normal Linux user UID 1000 not created yet; first-launch setup is next, requiring
the user to choose their local username/password. Docker and simulator remain
uninstalled in WSL. Do not claim runtime ROS/Gazebo validation.
