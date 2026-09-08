# Competition requirements — verified 2026-09-07

## Sources

- [RIT competition page](https://www.rit.edu/dubai/emirates-robotics-competition): simulation deadline September 15, 2026; updated September 3. Undergraduate competition; registration deadline June 30.
- [Official Phase 1 PDF](https://www.rit.edu/dubai/sites/rit.edu.dubai/files/docs/Emirates_Robotics_Competition___Edition_4__Phase_1_.pdf), obtained via RIT's current Phase 1 link; all eight pages inspected, scoring/revision pages also requested visually. Local sources/official-phase1.pdf SHA256: a21d9e250756c590c44e04829839171a21762eeb2a45ca5dbb70776691cba956. Revision table prints v1.0, 05/08/2025 despite 2026 title. Do not invent a newer revision date.
- [Official README](https://github.com/dfl-rlab/erc_sim_2026/blob/main/README.md), Dockerfile, up.sh, Compose and gripper relay inspected. Main SHA 2aa5a4a7d19177e0bb6625ea5f2c37f7b32bd33a.
- [Releases](https://github.com/dfl-rlab/erc_sim_2026/releases): latest v1.0.3, August 24, 2026, SHA 0a09806ecbade5edc9f8a148b7c9f439ed761554. Earlier v1.0.1 and v1.0.0. Local official clone pinned to v1.0.3; main documentation separately archived.
- Raw API responses and comments saved in sources/. All-state issues returned five entries including two PRs, below the 100-entry page size; every entry with comments was retrieved.

## CONFIRMED OFFICIAL REQUIREMENTS

PDF sections 1.2–1.5: use provided TIAGo Pro, one arm only. Live vision must identify randomized numbered columns and colored books; navigate, grasp, return, visually identify red collection bin and deliver. Five columns, six rows, four occupied rows, twenty books; each color once per column. Books vary horizontally between 25–75% of row width. Starting heading must be handled autonomously.

Provided container uses Ubuntu 22.04, ROS 2 Humble, Gazebo Harmonic. Preserve environment/robot. Additional packages such as IDEs may be installed, but submissions depending on modifications to the environment will not be evaluated. Simulator launches separately:

```bash
ros2 launch erc_bringup simulation.launch.py
ros2 launch aurak_erc_solution solution.launch.py shelf_column_number:=2 book_colour:=red
```

The second command is our future interface, NOT implemented yet. Support labels 1–5 and red/blue/green/yellow. Our launch must not start another simulator.

PDF sections 2–3: submit GitHub link with all solution ROS packages, launch file, package.xml dependencies and README. Video: YouTube link, <=5 minutes, unedited and not sped up, team name visible before trial, simulator then solution launch, visible timer throughout trial. Report: PDF <=5 pages excluding title page; ordered sections Architecture, Perception, Navigation, Manipulation, Results, Limitations/Future Work. Include detection accuracy, travel times, RViz planned/executed paths, scores across five trials, grasp success and average completion time.

| Scoring stage | Points / condition |
|---|---|
| Column | +1 publish, +2 annotated live image |
| Navigate to shelf | +3 awarded after successful grasp |
| Row (1–4) | +1 publish, +2 annotated live image |
| Pick | +3 |
| Return carrying book | +3 awarded after delivery |
| Bin delivery | +2 drop OR +4 gentle placement |
| Unintended collision | -0.5 per event, total floored at zero |

Derived maximum: 19 gentle / 17 dropped. Intentional grasp/place contact is distinct from unintended collisions. Continuous contact is one event; a new penalty needs separation and one-second same-object cooldown. Timer: solution launch to target-book/bin contact. Time breaks ties. Qualification: trial 50%, code 20%, video 10%, report 20%; best of three evaluator trials.

Evidence must be captured by our node DURING trial from live camera, stored in repository erc_images/, with bounding box around target column/book and timestamp in image. Our additional decision adds timestamped filenames and labels. No offline/manual images. User's engineering restrictions remain binding even when not verbatim in PDF.

## CONFIRMED SOFTWARE INTERFACES

Documentation-confirmed only; NO runtime checks yet. Details in ROBOT_INTERFACES.md.

Required outputs: /erc/shelf_column_identification and /erc/shelf_row_identification, std_msgs/msg/Int32. Column is recognized numerical label, not physical left-to-right index. Row is 1–4; direction unresolved.

README: AMD64 Linux, X11, Docker Engine/Compose v2, Git; Ubuntu 22.04 or 24.04 host recommended. We choose 22.04. NVIDIA optional, ~15 GB free prerequisite, ROS_DOMAIN_ID 23. Official up.sh falls back to integrated/software rendering, Compose maps /dev/dri. Up.sh pulls base image and Dockerfile installs apt packages: an uncached first build needs network despite README's broad no-network-after-cloning statement.

## Official issues/releases

- [#2 OPEN](https://github.com/dfl-rlab/erc_sim_2026/issues/2): gripper/effort/slipping. v1.0.3 changed book width/friction and limits; participant failures persisted. September 4 collaborator proposed issue_gripper_effort branch at 8b5f26187d17172aed8877ec4b21d8ecd239a848. September 6 collaborator reverted mesh problems at 4e0ce63b22e205392e33e732d9dbcf66ce36eaeb, awaiting confirmation before main merge. Baseline grasp is NOT proven. Latest collaborator says physical book spine is 2 cm, superseding PDF's 3 cm. Inspect chosen revision's actual dimensions.
- [PR #3 merged](https://github.com/dfl-rlab/erc_sim_2026/pull/3): width/friction/gripper limits, v1.0.3. No local simulator patches.
- [#4 closed](https://github.com/dfl-rlab/erc_sim_2026/issues/4): collaborator says Nav2/MoveIt are PRE-INSTALLED, not task-configured. Team must configure them.
- [#5 closed](https://github.com/dfl-rlab/erc_sim_2026/issues/5): collaborator says Phase 1 uses supplied left-facing orientation; retain robust handling of other headings.
- [PR #1 closed, unmerged](https://github.com/dfl-rlab/erc_sim_2026/pull/1): participant foundation work, not official solution policy.
- No other Intel, Docker, installation, camera or crash issues in returned inventory. Absence of reports does not prove compatibility. README covers DDS warnings, spawn delays, controller build, strafing and mixed build flags.

## ASSUMPTIONS

Intel rendering and Ubuntu hardware support will be usable: untested. Runtime topic/action/QoS/frame names may differ. Approved stable grasp fix availability unknown.

## IMPLEMENTATION DECISIONS

Use aurak_erc_solution; separate perception, navigation, manipulation, safety and evidence. Perception points first. Bounded retries, feedback, zero velocity on failure, one tested arm. No unauthorized physics changes, reference dependency, privileged perception, fake grasp or success. Choose release baseline, recheck upstream after reboot.

## UNRESOLVED QUESTIONS

1. Row numbering direction: text defines 1–4 but not top-to-bottom versus bottom-to-top. Inspect official assets/figures; ask organizers only if unresolved before implementation.
2. Which released/merged grasp update will judges use? Recheck #2/releases before implementation.
3. Runtime gripper actions/feedback, MoveIt/Nav2 functionality and sensor QoS.
4. PDF hardware LiDAR range 10 m differs from README simulation range 25 m; use actual messages for configuration.
5. Ubuntu hardware/graphics viability, encryption and firmware settings.

## Unofficial reference

[SaberFaceLove](https://github.com/SaberFaceLove/erc-competition-2026) package, launch, solution and tree inspected; cloned separately. No LICENSE in tree; package license TODO, API license unspecified. No substantial reuse permitted on current evidence.

Confirmed flaws: column method publishes requested number without digit recognition; timed driving; row derived from image-height quarters rather than shelf geometry; color search lacks target-column restriction; gripper closes without an arm grasp; fixed absolute evidence path; timestamp only in filename; unconditional completion; blocking sleeps/stale image risks. Its photos are not our evidence. Use only for interface discovery and independently implement.

## September 8 official update — supersedes older pending-merge note

At 2026-09-08T09:36:51Z, the official collaborator in issue #2 states the grasp fix
was tested and merged to main. API main now resolves to
93554d4f9335b2ee3acb49c6b332611f6ad2a964 (PR #6, September 8 09:34:09Z), increasing
gripper/book friction and reducing spine width to 2 cm. Latest tagged release
remains v1.0.3. Local v1.0.3 clone unchanged. Before simulator setup, use current
organizer guidance for baseline selection; do not assume release/main equivalent.
Source: https://github.com/dfl-rlab/erc_sim_2026/issues/2
This is an organizer report, not a grasp test performed by our team.
