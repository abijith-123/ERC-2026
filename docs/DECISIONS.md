# Decisions — 2026-09-07

- Honor the Windows stop boundary: review/document only; native Ubuntu must precede simulator installation and robot coding.
- Manual dual boot preserving Windows; recommend 150 GiB development space, distinct from official ~15 GB simulator prerequisite. Never alter encryption/partitions/boot automatically.
- Official RIT PDF and dfl-rlab sources win. Distinguish collaborators' statements from participants' reports. Recheck after reboot.
- Latest release currently v1.0.3; main is newer. Begin with latest official release at installation time. Do not silently substitute experimental gripper branch for judging baseline.
- Try integrated/software rendering through unchanged official scripts. No NVIDIA packages.
- Nav2/MoveIt configuration and gripper operation require testing. Select one arm after reachability testing.
- Provisional package aurak_erc_solution; perception scoring first after basic robot controls work.
- No source reuse from unofficial reference: license unspecified. Reference snapshots are local research, excluded from audit Git history.
- Linux layout: ~/erc2026/official/erc_sim_2026; ~/erc2026/references/SaberFaceLove-erc-competition-2026; ~/erc2026/submission; ~/erc2026/evidence; ~/erc2026/progress for this audit.
- Clean submission will contain our packages, package.xml dependencies, README, solution.launch.py and erc_images; no reference checkout dependency. Final colcon nesting follows integration testing.
- No GitHub push, public repository or organizer message authorized/performed.

## 2026-09-08 scope update
User paused USB/native Ubuntu work and explicitly approved Windows-compatible development. This supersedes the earlier no-coding-on-Windows checkpoint. Develop and test pure logic and package scaffolding now; runtime ROS/Gazebo validation remains mandatory before claiming robot features work. No WSL installation, disk changes or simulator environment modification implied.

## WSL fallback authorized
User explicitly requested 'Ok Do WSL2'. WSL2 with Ubuntu 22.04 is now the authorized host fallback; native USB installation remains paused. Test official Docker unchanged where possible, record any WSLg/graphics limitations. Windows feature installation and a required restart are expected; do not alter partitions or disable encryption.
