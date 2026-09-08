# WSL robotics environment

Verified on 2026-09-08, Windows 11 Surface Laptop 4.

- Ubuntu 22.04.5 under WSL2, default user `biju123` (UID 1000).
- WSL 2.7.13.0, kernel 6.18.33.2-microsoft-standard-WSL2, systemd enabled.
- Host `glxinfo -B`: accelerated D3D12 Intel Iris Xe, Mesa 23.2.1, OpenGL 4.1.
  This does not yet establish graphics support inside the simulator container.
- Docker Engine 29.8.0, Compose plugin 5.5.1, official Docker Jammy apt repository.
  User is in the docker group; `docker run --rm hello-world` passed.
- Linux official checkout: `/home/biju123/erc2026/official/erc_sim_2026`.
  Detached at organizer main `93554d4f9335b2ee3acb49c6b332611f6ad2a964`, containing
  the merged gripper fix. Windows release checkout remains at v1.0.3.
- Linux submission clone: `/home/biju123/erc2026/submission`, copied by Git bundle
  from the Windows submission repository, commit `a7dfe26`.
  These are independent clones; synchronize deliberately before further edits.
- Build log: `/home/biju123/erc2026/progress/simulator-build.log`.

Docker installation followed https://docs.docker.com/engine/install/ubuntu/ .
The official `docker/up.sh --build` completed successfully. All 32 official
packages compiled with `colcon build --symlink-install --parallel-workers 2`.
The official GUI simulation launched and the team's separate overlay package
received fresh camera frames (`CAMERA_READY`). Seven controllers were active.
Read-only inventory of topics, nodes, services, actions, hardware, controllers,
parameters and TF completed with all eight command exit codes zero.

## Graphics and persistent runtime

The unchanged Docker configuration used llvmpipe software rendering. A 12-second
sample measured real-time factor 0.224. Exposing `/usr/lib/wsl` read-only and
selecting d3d12 enabled Intel Iris Xe rendering, but measured factors were 0.086
and 0.076. These short runs used independently randomized layouts, so they are
diagnostic measurements rather than a controlled benchmark. Software mode was
restored because it performed better in these checks. Real-time performance
is NOT achieved; further host/rendering optimization remains open.

Local host override: `wsl/docker-compose.wsl.yml`, copied to
`/home/biju123/erc2026/runtime/docker-compose.wsl.yml`. It keeps compiled official
build/install and the team overlay in persistent host folders and exposes the
team submission read-only. Robot/world/physics source was not modified. Original
container was recreated after preserving compiled artifacts; temporary root
filesystem diagnostics were copied out as needed. No user files were deleted.

Use this in Ubuntu to start the configured container without rebuilding:

```bash
cd ~/erc2026/official/erc_sim_2026/docker
docker compose -f docker-compose.yml -f ~/erc2026/runtime/docker-compose.wsl.yml up -d --no-build
```

Start the simulator only if no simulation is already running:

```bash
docker exec -it erc_sim /entrypoint.sh bash -c 'source install/setup.bash && ros2 launch erc_bringup simulation.launch.py'
```

The team overlay is at `/opt/team_ws/install/setup.bash` inside the container.
It was rebuilt at submission ab7ea26 with live perception and a motion watchdog;
autonomous navigation/grasp/delivery remain incomplete. Linux submission is now
synchronized to ab7ea26. Launch from a writable submission copy, or specify a
writable repository with ERC_OUTPUT_ROOT, because /opt/team_submission is read-only.
Do not rerun official up.sh casually: it removes the container and omits the local
override. The current simulator is left running, with log at
`/home/biju123/erc2026/progress/simulation-scene-02.log` (latest restart).

Additional checks completed in temporary ROS Humble containers:

- ROS base image digest: `sha256:b624d8bcea33796d32e0dbd85326722188485759bbd6b538e4785750a5c88a7b`.
- Python 3.10.12, NumPy 1.21.5, OpenCV 4.5.4, Pillow 9.0.1.
- All 37 offline tests passed; log `sources/linux-offline-tests.log`.
- Submission package built and installed with colcon. Installed launch exposes
  exactly shelf_column_number and book_colour. With no camera or simulation
  clock, its node reports PREFLIGHT_FAILED and exits with code 1 within the
  bounded check. Log `sources/ros-package-check.log`.
- No simulator was launched by these tests, and no competition evidence was made.

Open Ubuntu from Windows with `wsl.exe -d Ubuntu-22.04`.
First-use account creation is complete. No additional restart is currently needed.

Ubuntu download workaround: automatic WSL downloads stalled at zero bytes;
direct IPv4 download from Canonical succeeded and was checked against the SHA256
in Microsoft's WSL distribution catalog before installation. Apt host commands
also used Acquire::ForceIPv4=true, without changing global network settings.
