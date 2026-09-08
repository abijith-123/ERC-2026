# Test results — Phase 0

| Check | Result |
|---|---|
| Running OS/architecture | PASS: Windows 11 Pro, Intel x86-64 |
| CPU/RAM/GPU/storage measurements | PASS: JSON saved |
| Native Ubuntu currently running | NO: Windows; no Linux partition detected internally |
| Firmware virtualization setting | INCONCLUSIVE: hypervisor present masks capability reporting |
| BitLocker status / boot entries | BLOCKED: read access denied |
| Official README/PDF/issues/releases fetched | PASS: raw files saved, PDF SHA256 recorded |
| Reference license/implementation review | PASS: no clear reuse license, flaws documented; no reuse |
| Portable Git | PASS: version 2.55.0.windows.5 |
| Repository clones | PASS: official v1.0.3 and separate reference |
| Required documentation presence | PASS: all nine required documents exist and are nonempty; PDF hash matches |
| ROS/colcon/Gazebo tests | NOT RUN: explicit Windows checkpoint |
| Simulator FPS/rates/RTF | NOT MEASURED |
| Robot controls/perception/grasp/trials | NOT IMPLEMENTED / NOT RUN |

No trial metrics, evidence images, or mission success have been fabricated. Source snapshots are research evidence only. Documentation checks do not validate robotics functionality.

Ubuntu media preparation: ISO SHA256 PASS, Rufus Authenticode Valid (Akeo Consulting). USB bootability NOT TESTED; media not written yet.

USB structural check PASS: expected device serial, GPT/FAT32, Ubuntu release identity and EFI/kernel/initrd/GRUB files present. Actual boot and hardware compatibility still NOT TESTED.

## 2026-09-08 Windows development milestone

User explicitly authorized coding on Windows while USB work is paused.

- PASS: 23 offline tests, both original submission and fresh local clone.
- Coverage: 20 column/color requests; 120 marker-label permutations; illegal state
  skips; exact timeout boundary; bounded retries; preserved failure cause; explicit
  delivery confirmation; stale/future/duplicate camera stamps; continuous collision
  events; actual synthetic PNG file rendering; invalid paths/boxes; metrics integrity.
- PASS: Python 3.10 syntax parsing for package and launch, package.xml dependencies,
  exactly two launch arguments with no defaults or simulator include (static only).
- PASS: pip wheel build; expected ROS launch/config/resource metadata included.
- PASS: built wheel CLI from isolated temporary cwd accepts valid request and rejects
  column 0. Empty real results directory produces zero trials with null percentages.
- PASS: fresh local clone tests (not a fresh OS or official-container trial).
- NOT RUN: colcon build/test, ROS launch, camera preflight, live perception, motion,
  navigation, arm/gripper, grasp, bin delivery, graphics or any competition trial.

Runtime: bundled Python 3.12.14 on Windows, Pillow already installed. pytest and
PyYAML absent; standard-library unittest used. Initial evidence test failed because
Windows temporary root used short versus resolved path spelling; test comparison
fixed and suite passed. Initial setup.py wheel build warned about deprecation;
subsequent pip wheel --no-deps --no-build-isolation succeeded.

Logs: sources/windows-foundation-tests.txt, sources/windows-clean-clone-tests.txt.
Source commit c534b2f in separate submission repository. Synthetic data exists only
in auto-cleaned temporary directories, never in submission/erc_images or results.

## Vision/alignment milestone

37 offline tests PASS (Windows Python 3.12, NumPy, Pillow, OpenCV 4.10.0.84), also
PASS in fresh local clone .tools/vision-validation-20260908. Wheel build and isolated
CLI pass. Tests cover image encodings/stride/endianness, synthetic glyphs, color ROI
exclusion, red hue wrap, invalid/median depth, bin-size proposals, temporal stability,
alignment clamping/convergence/zero on failure. Source commit a7dfe26.

Exploratory flat official texture probe: initial templates accepted 1–3, stroke
variants accepted 1–4; 5 rejected as ambiguous with 3. These five development inputs
are not held-out and not rendered camera images. No live detection accuracy claimed.
Raw diagnostic: sources/official-texture-diagnostic.json. Logs: windows-vision-tests.txt
and windows-vision-clean-clone-tests.txt. Full mission remains INCOMPLETE.
