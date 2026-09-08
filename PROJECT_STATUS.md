# PROJECT STATUS

Updated 2026-09-08. Current phase: Windows-compatible solution foundations.
STATUS: PASS for offline foundation milestone; ROS/Gazebo integration NOT RUN.

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
Submission implementation commit: c534b2f (feat: add tested ERC mission foundations and camera preflight).
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
MoveIt/Nav2 setup and gripper behaviour unverified. Official #2 grasp issue was
open September 7 with an experimental September 6 patch, not established baseline.
Row numbering direction still unresolved; helper requires explicit top-row number.
Maintainer contact is placeholder; proprietary license is provisional, no public
license chosen. Deadline last verified on RIT page: September 15, 2026.

Commands/results: docs/COMMANDS.md, docs/TEST_RESULTS.md. Evidence logs are in
sources/windows-foundation-tests.txt and sources/windows-clean-clone-tests.txt.
