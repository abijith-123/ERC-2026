# ERC development demonstration

Status: **incomplete competition entry — no verified book delivery**.

## Executed in the official simulator

| Step | Evidence |
|---|---|
| Right-arm lift | Action success, final joint feedback checked; 15.20 simulated seconds |
| Forward approach with raised right arm | Odometry goal reached; no detected external contact |
| Right-arm pregrasp | Action success, final joint feedback checked; 3.91 simulated seconds |
| Automated checks | 51 passing tests |
| Fresh randomized scene05 approach | Column5/blue identified and reacquired; 203.50 s wall time; no grasp attempted |

These were development diagnostics in scene04. The book remained on the shelf.
The following image is the robot's actual camera view after right-arm alignment,
not a generated illustration and not proof of a successful grasp.

![Robot camera, scene04](docs/sources/live-camera-scene04.png)

Logs: [arm lift](docs/sources/right-arm-lift-01.log),
[raised-arm approach](docs/sources/raised-arm-approach-01.log),
[pregrasp execution](docs/sources/pregrasp-aligned-01.log).

## Still required

- Validate finger insertion, physical pinch and book retention.
- Integrate manipulation into the autonomous mission and verify delivery.
- Confirm row numbering and complete five randomized full trials.
- Produce the final competition report and unedited demonstration video.

Gazebo exited on an X-server error after the pregrasp. The simulator was restarted
with the organizer's headless mode. Old scene coordinates and plans are invalid.
See [project status](PROJECT_STATUS.md) for the latest running trial and results.
