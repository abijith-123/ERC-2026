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
The official `docker/up.sh --build` was launched unchanged. Build completion,
container graphics, colcon and live simulator checks remain pending.

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
