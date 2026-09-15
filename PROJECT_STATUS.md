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

## 2026-09-12 manipulation diagnostics (not competition complete)

Scene05 later segfaulted in Gazebo EntityComponentManager::ProcessRemoveEntityRequests.
Restarted unchanged official headless simulation as scene06, PID10156/10177,
log ~/erc2026/progress/simulation-scene-06.log. Planner PID11137/11159 uses
the updated shoulder adjacency pairs and 0.06 m self-filter padding.

Fresh navigation trial20260910T053353-3efa5a passed for column5/blue, top index3.
Its same-scene checkpoint is results/observations/20260910T053353-3efa5a.approach.json.
Grasp diagnostic20260910T054035-63ba7c performed lateral alignment, lift,
closer approach and pregrasp. Planar base candidate validation now explicitly
sets multi_dof_joint_state.header.frame_id='odom'; the earlier omitted frame
was caught from MoveIt warnings and the active arm motion cancelled before
allowing further base motion. Added a regression test for the candidate frame.

Grasp stopped at absent planning-object removal; fixed to check existing objects
before REMOVE. Subsequent insertion cancelled on physical finger/book contact.
Observed contact identity: book_col_5_row_4_blue with right fingertip_left.
Only the identity is used to scope physical contact allowance; encoded column,
row and colour fields are not read for target localization.
Actual stopped hand was about (1.0417,-.4363,.9968) vs book center near .92 m high.
Camera capture .tools/wsl/insertion-contact-06/rgb.png shows the open hand at book.
Cartesian recovery returned 3.85% and was rejected. Joint-space recovery is
currently running as exec session48854, log target-contact-grasp-06.log.
No verified pinch, retention or delivery yet. 64 tests pass. All new grasp,
delivery and clearance components remain development-stage software.

Recovery session48854 has finished and no motion controller is running. The
19.40 sim-second withdrawal completed, but fresh RGB showed the blue book now
lying flat on the shelf. The upright-book reacquisition gate rejected it and
no pinch was issued. This attempt FAILED; do not reuse its upright target
geometry. Evidence: docs/sources/book-toppled-scene06.png and
docs/sources/target-contact-grasp-06.log. Robot remains stopped in scene06.
Next manipulation work must fix approach geometry/IK branch continuity and
avoid toppling the target, then validate a physical pinch in a fresh scene.
The complete autonomous delivery pipeline, five full trials, report and video
remain unfinished. There is no competition-ready version to deliver yet.

## 2026-09-12 scene07 reach and Cartesian diagnostics

Unchanged official scene07 and MoveIt planner are running. Fresh navigation
20260911T211116-2a4739 passed for column5/blue. Revised book lateral alignment
y=-.30 and right-arm lift (.60,-.30,observed height) executed. Whole-body checks
blocked the proposed x=.85 book staging distance on idle left-arm/shelf geometry.
Planning-only torso sweeps 0..35 cm found no clear 40 cm advance. Shorter guarded
advances brought the observed book to x=.99 without detected external contact.
Straight pregrasp executed; live evidence docs/sources/pregrasp-scene07.png.

Insertion requests returned 88.9% then92.3% and were never executed. Controlled
planning-only comparisons with identical collision checking isolated the relative
jump threshold: threshold2 returns92.3%, threshold0 returns100%, for yaw0 and the
observed shelf yaw. Largest returned timed waypoint delta was .025 rad. Cartesian
planning now uses threshold0 with an independent cumulative1.5 rad per-joint travel
limit, existing sampled collision checks and bounded action execution. Empty/wrong
frame maps are now explicitly rejected for Cartesian planning. 66 tests pass and
the dev overlay builds. Retry07d is active in exec session21919,
~/erc2026/progress/observed-grasp-07d.log. No verified pinch or delivery yet.

## Scene07 physical pickup and return passed; bin work active

Retry07e physically pinched the observed blue book. Checkpoint
results/20260912T080434-b2a2c8.pinch.json records opposing contacts with the opaque
identity book_col_2_row_4_blue and blocked gripper opening .00506 m. Never decode
that identity for target localization. Lift12 mm passed; withdrawal20 cm timed
out after roughly17 cm because the simulator was slower than8x wall time.
Retention remained present; a guarded4 cm continuation passed and wrote the
same-prefix .retention.json. Base return wrote .return.json at approximately
(.0046,-.0083,-1.5655), within1 cm of the recorded start position. All motions used
physical contact retention guards. No Gazebo attachment/pose/physics changes.
The MoveIt attached object is carried collision geometry only, not a physical
constraint. Evidence: carried-book-scene07.png, observed-grasp-07e.log,
book-retention-07.log, book-retention-07b.log, carried-return-07.log.

Head-only bin scan /tmp/bin-scan-07 found no candidate in three forward/side views.
Turn attempts stopped on the wider1.15 m laser clearance guard. Investigation
found a real laser transform bug: official scanners have roll pi, but old code
used yaw alone. Full quaternion projection now fixes mirrored obstacles; regression
test added. Earlier full navigation must be revalidated after this fix. Nearby
objects are behind the robot, not the idle arm (initial hypothesis disproved).

Another guard exposed floor voxels colliding with wheels at z=.028 m. New
planning_cloud node transforms raw depth through the validated actual render
mount into odom and excludes the flat ground plane below25 mm, preserving obstacle
checks on all links. Planner restarted with this node; carried collision geometry
saved/restored via /tmp/carried-planning-scene07.bin. No simulator restart.
New planner session16395, launchPID14834, filter14856, MoveIt14858,
log moveit-scene07-calibrated.log. Official server remainsPID12343/launch12322.
72 tests pass; dev overlay builds. A further35 cm forward clearance move followed
by a guarded180-degree turn is running in exec session67404. Robot started at
(.2354,-.2562,-1.5655); move goal(.2372,-.6062,-1.5655). Book remains physically held.

Submission source latest committed bd4fa96, with subsequent laser/turn/cloud
changes not yet committed. Linux clone is older e2ec4bb until next sync.
Bin detector now exists with metric floor/size gates and full-rim requirement,
but needs live validation. Delivery, integrated full mission, five full trials,
row convention, report and video remain incomplete. Do not claim final readiness.

## Scene07 physical delivery VERIFIED (latest)

The carried turn passed after the second clearance move, ending near
(.2372,-.5962,1.5956). The camera found the red bin ON A TABLE, disproving the
initial floor-bin assumption. Live RGB/depth measured footprint approximately
.56 by .31 m, bottomz.74 and topz.95. The scoop's front lip is lower than its back,
so fitting only a horizontal top rim was wrong. Bin vision now fits the complete
observed footprint with all four corner supports, known metric dimensions and
height gates. A1-pixel colour-mask erosion rejects mixed RGB/depth boundary pixels
that otherwise included background floor points and inflated the rectangle.

Torso lift to .189048 m passed with physical retention monitoring and a hold-on-
failure command. Diagonal table approach was rejected on idle-left-gripper
geometry. Planning-only candidate tests found lateral-first alignment to book/bin
y=-.4 then advance to bincenterx1.15 clear, with reachable drop IK. Both base legs
executed. The held book occluded the bin; right hand moved to(.70,-.60,1.12115),
retention passed and the whole bin became visible. Three fresh frames gave
bincenter(1.15663,-.38810,.94947), all corners recorded in results/bin-staging-scene07.json.

Physical placement used a collision-checked joint-space path after the Cartesian
travel bound rejected the long movement. It passed149 waypoints/209 samples,
14.79 simseconds. Measured release toolpose(1.03669,-.38397,1.09947) passedfeedback,
then gripperopened .055. /bin_contacts verified the SAME opaque contacted book
book_col_2_row_4_blue against erc_collection_bin continuously >=2 simseconds with
no robot/book contact. Result: results/physical-delivery-scene07.json. Evidence
copied to docs/sources/physical-delivery-scene07.json and its executionlog07b.

After delivery, removed only MoveIt carried-object bookkeeping, refreshedmap and
withdrew the openhand to(.85,-.50,~1.09947). No Gazebo model or physics changes.
Final camera docs/sources/delivered-book-scene07.png visibly shows blue book in bin.
Robot stopped at base(-.32306,-.22191,1.59339), torso.189048, gripper.055,
headpan0/pitch-.5. No motion diagnostic or watchdog running. Official scene07
and MoveIt remainrunning; the camera-cloud node was separately restarted to
preserve the actual optical sensor origin for correct Octomap ray tracing.
Planner session16395 remains; cloud session68461 remains. New source defines
erc_planning_optical TF at the actual render mount; floor filtering is evaluated
in odom, but filtered output stays in optical coordinates.

Found a final placement-model detail: GetPlanningScene stores the .055 m carried
book offset in CollisionObject.pose, with identity primitive pose. The successful
run ignored that offset but still physically delivered inside the roomy bin.
Updated placement_goal now composes both poses and checks all eight book corners
with25 mm footprint margin and bottom clearance. This correction has unit coverage
but has not yet been used in a second live delivery. 75 tests pass. Latest code
is being committed/synced; use git HEAD instead of earlier revision notes above.

THIS IS ONE LINKED DIAGNOSTIC SUCCESS, not an uninterrupted competition trial.
solution.launch.py still stops after navigation. Required next work: integrate
all stages, generalize collision-safe staging across rows/columns, revalidate
after sensor fixes, five full randomized trials, official row convention, report
and unedited video. Do not claim the complete entry is ready.
Some diagnostic JSONs currently live at results root alongside TrialResult files;
move future diagnostics to a separate directory before using offline summarize,
which strictly expects only TrialResult JSONs at root. Duplicate nested evidence
backups were retained after an optional cleanup command was policy-blocked.

Final save: submission commit e5c3390, synced to Linux clone and container; both
dev and persistent overlays build. 75 tests passed; new placement scripts compile.
Planner launch14834/MoveIt14858 and standalone cloud15121/15143 remain running.
No motion controller is active. Raw results/images copied to Windows and Linux
progress/checkpoint-scene07. No GitHub push or submission has been made.

## 2026-09-13 — integrated mission validation underway

User will handle recording. Added manipulation.py, bin_approach.py, placement.py to connect pickup, continuous-retention withdrawal, return to the true pre-search start, bounded visual bin search/staging, and physical placement in complete mode. solution.launch.py includes planning.launch.py only in complete mode; never start a second planner. Completion and result exit status require the verified terminal state; first failure is preserved. Confirmed row convention is still required for complete status. Checked-in mission.yaml remains navigation pending live validation; the dev container copy is complete for testing.

Added simulation-time base velocity ramp (planar acceleration .15 m/s², angular .30 rad/s²) to the independent watchdog. Explicit zero command, expired lease, stale sensors and clock rewind immediately zero output. Four profile tests pass. Fixed approach checkpoint to preserve self.start_pose before search, and evidence to use the actual snapshot acquisition metadata. Offline summary explicitly lists stage-evidence JSONs separately, retaining all failed TrialResult files and rejecting malformed trial records. Updated previously stale report draft and architecture.

84 tests pass in the official container. Build passes. Live command sample docs/sources/scene08-velocity.csv contains 501 samples over 4.608 simulation seconds (25 wall seconds), 357 nonzero, maximum planar speed .18 m/s. This is command evidence, not a completed smoothness/reliability evaluation.

The prior container/simulator was stopped across sessions. Persistent attached container shell exec19041 keeps erc_sim available. Fresh unseeded official scene08 launch exec76794, log ~/erc2026/progress/simulation-scene-08.log. First complete attempt exec91769 failed before motion with missing depth (result 20260913T000647-db5a7e). Gazebo depth transport was publishing, but official camera bridge delivered no ROS depth. Restarted only that bridge using its original parameters; depth restored ~6 Hz. This restarted bridge exec1131 logs restarted-camera-bridge-scene08.log. Original camera bridge PID123 was interrupted. No robot/world/physics/randomization changes. MoveIt emitted a teardown segmentation fault on the failed attempt.

Second complete attempt exec15615, log ~/erc2026/progress/complete-scene08b.log, requests column2/red. It detected the randomized target in the lowest occupied row, navigated, reacquired, and entered PREPARING_GRASP. At this note it is still executing; inspect log/processes before commanding anything. Original separate planner exec69869 was stopped; the complete solution now owns planner and watchdog. Do not reset the scene or launch another motion controller while it is active.

Report remains a draft, five full trials and clean-clone full delivery are unverified, recording belongs to user, no public push. Source has new integration that has unit/build validation but not yet a full live delivery. Save runtime results/logs after the current attempt. Official PDF was rechecked online: it specifies occupied rows1–4 without direction; source active physical rows use a different whole-shelf index. Do not infer runtime localization from book contact names.

## 2026-09-15 continuation — lower-row clearance and startup fixes

Integrated attempt scene08b failed safely with no collision-free IK for a low (.60,-.30,~.60) arm staging pose. Diagnostic scene08c successfully executed a higher (.60,-.30,.95) staging trajectory (16.26 simulation seconds), but whole-body validation rejected the next advance because the idle left gripper would intersect the shelf. No left-arm command or collision-check bypass was used.

Read-only planning probes found a complete checked path to the higher staging pose. Further whole-body samples showed front-book standoff 1.07m clear and 1.06m blocked in this scene. manipulation.approach_book now searches a bounded .98..1.12m grid, moves only after the entire segment passes, and propagates missing/stale planner errors instead of treating them as obstacle alternatives. It also skips a staging arm move if feedback is already within8mm; free-space pregrasp may use a fully collision-checked RRT path, while insertion stays strictly Cartesian. Diagnostic reach-only IK probes did not execute unvalidated trajectories.

The Sept15 retry scene08d failed before movement because TF had not joined the camera to the robot when sensor readiness first passed. wait_ready now also requires the observed camera-render transform; reacquire_book aims from that calibrated mount. Retry scene08e is active (exec89070), log ~/erc2026/progress/pickup-scene08e.log, using checkpoint observations/20260913T094931-44629d.approach.json. It is a diagnostic, never count it as a full run. Check log before new motion commands. The external planner1659 and official simulator117 remain available; camera bridge was separately restarted earlier.

Standard colcon test was initially discovering zero tests. Added tests_require pytest and testpaths configuration. Correct command: cd /opt/dev_ws && colcon test --base-paths /opt/dev_submission/aurak_erc_solution --packages-select aurak_erc_solution && colcon test-result --verbose. It now reports 87 tests,0 errors,0 failures,0 skipped. Direct pytest also previously passed84 tests; new tests cover TF startup and refusal to move when all approach paths collide or the planner is unavailable.

Created a reproducible five-page development PDF (title +4 content pages), submission/output/pdf/erc-technical-report-draft.pdf, using scripts/build_report.py and the updated Markdown source. Rendered and visually checked every page; updated page4 rechecked. Clearly marked NOT READY FOR COMPETITION SUBMISSION. Contains actual scene07 delivery photo, limitations, unverified trial counts; user will record the video. PDF opened in Codex panel. The report snapshot says84 tests as of rendering; current suite87. Final report needs fresh full-trial results and the current diagnostic outcome.
