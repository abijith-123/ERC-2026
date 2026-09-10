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

User completed account setup: default user biju123 (UID 1000). Docker Engine
29.8.0 and Compose 5.5.1 installed from official Docker apt repository; user in
docker group. hello-world container passed. Host glxinfo confirms accelerated
D3D12 Intel Iris Xe OpenGL 4.1. See docs/WSL_SETUP.md for paths and limitations.
Official simulator clone in Linux pinned to organizer main 93554d4 (merged
gripper fix), submission clone a7dfe26 transferred by Git bundle. Official
./docker/up.sh --build is RUNNING, log at
/home/biju123/erc2026/progress/simulator-build.log. Do not start a duplicate build.
Container graphics, colcon, live simulator and mission preflight still pending.

## COMPLETE: WSL simulator setup milestone
Official Docker build succeeded. All 32 official packages compiled. Team package
also compiled and installed in separate /opt/team_ws overlay. All 37 offline tests
passed under actual Python 3.10/ROS Humble. Absent-camera launch correctly failed;
live simulation launch produced CAMERA_READY. Camera diagnostic was 640x360 rgb8;
no target recognition or competition success claimed. All seven controllers active.
Eight read-only interface inventory commands passed (docs/sources/wsl-first-inventory).

Current container erc_sim and official GUI simulation are RUNNING. Current log:
/home/biju123/erc2026/progress/current-simulation.log. Do not start a duplicate.
Read docs/WSL_SETUP.md before restarting; a local Compose override now preserves
build/install/team workspace folders across recreation. Official simulator source
remains unmodified at organizer main 93554d4. Windows submission and Linux clone
remain a7dfe26; no code changes were required during setup.

Performance limitation: final software-rendering factor 0.218 (about 4.6 wall
seconds per simulated second). Intel D3D12 rendering was enabled and verified but
was slower in short diagnostics (0.076); software restored. No physics/sensor-rate
changes made. NEXT: investigate performance and integrate actual live perception,
navigation, single-arm grasp/delivery. Current solution is still preflight-only.

## PASS: conservative robot baseline — 2026-09-08
Added RobotIO feedback primitives and scripts/verify_robot.py in submission.
Live baseline passed forward/back 0.10 m, strafe left/right 0.10 m, rotate/back
0.20 rad, head 0.15 rad/back, torso 0.03 m/back, right arm joint 1 0.05 rad/back,
public right gripper 0.04 m open/back closed. All endpoints checked using odometry
or joint states; zero base command sent in finally. Right arm is the provisional
tested arm, reachability and grasp still unverified. Saved baseline-motion.log.
RGB/depth/calibration/both lasers/odom/joints passed timestamp freshness checks.
Baseline initial laser clearance 0.741 m in base frame. All 37 existing tests pass
inside ROS. RobotIO arm limits are intentionally narrow baseline limits; do not
treat it as a full manipulation planner.
Active: scripts/scan_shelf.py is collecting live diagnostic images at head pitch
-0.2 and closed-loop 45-degree clockwise steps; no ERC output topics published.
Container dev copy is /opt/dev_submission; committed Linux submission clone is
still a7dfe26 until next bundle sync. Windows submission is canonical for edits.

## Live perception integration — 2026-09-08, active development
Submission commit ab7ea26 is synchronized to the Linux submission clone. Added
registered RGB/depth geometry, capture-time TF with buffered synchronization,
generic-font marker recognition, metric book association, three-frame evidence,
ERC column publication and an independent velocity watchdog. All 41 tests pass
under ROS Humble/Python 3.10. Isolated ROS domain 91 watchdog tests passed command
expiry, invalid-command rejection and stale-sensor stopping. Full delivery absent.

A frontal live diagnostic correctly recognized all five labels and twenty books
in the first scene. This is a development observation, not held-out accuracy.
Integrated runs exposed TF timing and combined translation/rotation drift; fixes
buffer one RGB frame and use angular-only feedback for search turns. A live turn
reached its heading with steady odometry position. Earlier interrupted/failing
runs saved incomplete results; no successful full trial exists.

Official simulation was restarted normally for a new randomized scene. Current
simulation launch PID 1927 (container), log ~/erc2026/progress/simulation-scene-02.log.
Active solution launch PID 2792, log live-perception-trial-05.log, testing the
corrected sweep from the normal start. Do not start duplicate motion controllers.
Dev overlay /opt/dev_ws; persistent overlay /opt/team_ws rebuilt from synchronized
read-only /opt/team_submission. Runtime dev output remains /opt/dev_submission;
copy results/images out before container recreation. Prior results backed up to
~/erc2026/progress/development-results. Row topic withheld until numbering clarified.

## Perception PASS; approach and arm planning development — 2026-09-09
Fresh scene 02 autonomous sweep found column 2/red, top occupied index 1, in
143 wall seconds. Live evidence visually checked; actual result correctly false
(perception-only). Next column 5/blue run found it in 7.5 seconds from the settled
view and reached a coarse depth-derived base approach. Evidence/results copied to
Windows submission/erc_images and results (ignored local artifacts). Logs saved
in docs/sources/live-perception-pass.log and live-navigation-pass.log.

Scene 03 edge-column approach timed out near its target during a tiny heading
correction. Fixed low-speed angular deadband; bounded small-angle live turn/back
passed. Head command validation corrected to official soft upper pitch 0.279 rad;
an earlier over-limit diagnostic saturated and required a fresh simulation.
Close RGBD association added with a strict 0.30 m prior-position gate and three
distinct stable frames. It rejects a larger same-color distractor and invalid
depth in tests. A manually approximated diagnostic prior was rejected after the
incomplete approach; no integrated close-approach success claimed yet.

Planning-only MoveIt configuration reads the official robot URDF. FK matched live
TF to numerical precision. Current fully lowered shoulder has ~0.8 mm body overlap;
this arm/body collision remains enabled. Parallel same-finger linkage contacts are
marked adjacent in SRDF. Some raised-torso IK queries succeed, others fail. No
environment collision geometry or arm trajectory execution implemented yet.

Submission d816e11 synchronized Windows/Linux/dev container. 42 tests pass under
ROS Humble. Current default development stage is navigation then close reacquisition,
and always records incomplete delivery. Current scene 04 is running; log
~/erc2026/progress/simulation-scene-04.log. Active solution launch PID 5832,
live-approach-trial-03.log, from fresh start with column 5/blue. Planning node stopped
before reset. Preserve dev results/images before recreating container. No full
competition trial has succeeded; row convention, actual grasp/delivery, five full
randomized trials, final report/video and submission still outstanding.

## CRITICAL calibration fix and close diagnostic PASS — 2026-09-09
Submission aa94f45 committed (Linux clone still d816e11 until next sync). Scene 04
remains running; current robot near shelf, odom about (2.1849,-1.9054,-1.5928),
head pitch -0.25. No motion controller active. Same-scene resume_approach diagnostic
reached saved goal and reacquired blue book over three frames; result
20260909T022838-cf3840 is intentionally incomplete/no delivery.

Investigating grasp exposed incorrect RGB/depth registration. Official URDF has
both camera render sensors at head_front_camera_link with no sensor pose offset,
while their gz_frame_id optical names have a 15 mm hardware-style TF offset.
Applying that offset shifted thin-spine depth into background. RobotIO now obtains
and validates render mounts from live robot_description, uses colocated depth
pixels, and transforms through the actual render link. Intrinsics must match;
changed mounts fail closed. No official simulator files modified. Live comparison:
foreground optical depth 0.849 m, projected book height 0.257 m; old shifted depth
sampled background near 1.05 m. Corrected base point about (.9324,.1484,.9301).
43 pure tests pass including model-mount mismatch rejection. Earlier recognition
evidence is valid, but earlier depth estimates must not guide a grasp.

Generic digit shear augmentation fixed a leftmost 5 failing the unchanged 0.07
ambiguity margin. Fine base control now rotates large angles first and combines
small yaw correction with translation, with minimum nonzero speed to overcome
stiction. Resumed approach passed using this control.

MoveIt live OctoMap works after installing declared ros-humble-moveit-ros-perception
2.5.9 (only new perception/freeglut packages, no ROS/Gazebo upgrade). Map verified
nonempty in odom, planar virtual joint present, FK agrees with live TF. Planning
launch disables execution. Right shoulder housing/torso mount contact now marked
adjacent; other arm/body collisions remain enabled. A pre-grasp proposal (.80,.148,
.93) with proposed torso .05 passed collision-aware IK/state validity; no arm moved.
Initial hand/map voxel overlap remains under investigation. Planner launch PID7167
currently runs previous self-filter padding .03; Windows padding .06 NOT deployed.
Dev sources otherwise include latest camera correction. Current simulator session
26708, planner session27431. Persist evidence and results before container recreation.

## 2026-09-09 contact recovery and planning update

Supersedes the runtime/planner details above. Live planning with 0.06 m self-filter
padding and time parameterization produced a planning-only right pregrasp path:
148 waypoints, 186 collision samples, 14.60 simulated seconds. No arm trajectory
was executed. The plan is now invalid because the base subsequently moved.

Physical contact inspection found the unused left forearm touching the shelf at
the old 0.95 m approach. New contact aggregation handles partial messages from
the thirty contact publishers; ordinary base motion and arm planning reject
active external contact. A bounded backward recovery stopped correctly when
contact changed from forearm to fingertip after about 8.8 cm. A second observed-
contact recovery cleared the shelf. Final odom approximately (2.1883,-1.7079,-1.6035),
with no active contacts. Neither arm was commanded during recovery.
Logs: docs/sources/contact-recovery-01.log and contact-recovery-02.log.

Initial staging distance changed to 1.25 m; this is conservative staging, not
validated whole-robot navigation. Fresh full approach still needs testing.
Live spine geometry and partial-contact tests bring the passing suite to 48.
Simulator PID4926 and planning launch PID7451 remain running; robot stopped.
Competition is NOT ready: physical grasp/delivery, full randomized trials,
row convention confirmation, final report and video remain incomplete.

## 2026-09-10 executed arm diagnostics and simulator restart

Scene04: additional left inner-finger contact stopped lateral motion; bounded
backward recovery cleared it. Lateral right-arm alignment then passed, followed
by a planned right-arm lift (154 waypoints/230 collision samples, 15.20 sim s).
FollowJointTrajectory returned success and final joints matched. Raised-arm
forward approach passed. Fresh visual blue spine front approximately
(1.0102,-.4722,.9199) in base gave a pregrasp 10 cm forward of the spine:
41 waypoints/51 samples, 3.91 sim s, executed successfully with feedback.
Neither completed arm motion detected external contact; neither is a grasp.
Logs saved in docs/sources/right-arm-lift-01.log, raised-arm-approach-01.log,
pregrasp-aligned-01.log. Detailed plans are in Linux progress/pregrasp-aligned-01*.

Insertion preparation opened the right gripper, created a perception-derived
MoveIt book object, and rejected a not-yet-rebuilt OctoMap. Fixed the wait to
require actual map data. Retry could not initialize sensors: Gazebo exited on
an XIO error and killed its server. Thus NO insertion/pinch/delivery occurred.
Stopped old launch processes and restarted official simulation headless:=true,
scene05 log ~/erc2026/progress/simulation-scene-05.log, exec session92315.
Fresh column5/blue navigation test session66796 is running. All scene04 plans
and observed coordinates are invalid for scene05. No official files modified.
51 tests pass. Arm action executor and insertion prototype remain development
tools; mission still stops after navigation and must not be called complete.

Scene05 fresh navigation completed: trial20260910T051902-ee6829 identified
column5/blue (observed top index3), approached at the revised 1.25 m staging
distance and reacquired the target. Total wall time203.50 s, navigation55.25 s,
alignment11.12 s. Saved result remains success:false/navigation_only with zero
grasp attempts; collision count remains null, not a fabricated zero. Robot is
stopped near odom(.1934,-1.5377,-1.5660); default arms, head tracking target.
Official headless simulator continues; no planner or mission process is running.
Windows results/images now include this trial; log docs/sources/fresh-navigation-05.log.
DEMONSTRATION.md shows verified progress and remaining requirements.
