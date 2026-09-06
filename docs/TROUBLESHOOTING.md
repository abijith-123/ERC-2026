# Troubleshooting

- Git missing: local .tools/mingit/cmd/git.exe works; tools directory excluded from Git. Reclone using Linux Git after Ubuntu installation.
- BitLocker/boot read denied: status remains unknown; check manually during installation preparation. Never assume encryption off. No recovery key should be stored here.
- Free disk space is not unallocated space: 368 GiB free C:, only 2 MiB unallocated. Follow UBUNTU_INSTALL_CHECKLIST.md before manual resizing.
- HypervisorPresent true conflicts with CPU feature fields false: cannot infer virtualization disabled from those fields.
- Windows/OneDrive checkout: research only. Use native Ubuntu filesystem for executable bits, symlinks, colcon and Docker work.
- Official #2 grasp issue is open. Experimental September 6 branch change is not current main/release. Recheck before designing manipulation.
- Public gripper relay versus raw controller: public topic enforces limits; discover actual action availability and do not bypass relay accidentally.
- Nav2 and MoveIt installed, not task configured (#4). No proof that default launch exposes planners.
- Integrated graphics: official up.sh supports fallback; do not add NVIDIA packages. Test unchanged first, then inspect /dev/dri, Mesa/OpenGL, X11 and official issues if failures occur.
- First Docker build requires internet despite README statement. up.sh recreates container; attach.sh opens extra terminals safely.
- Ubuntu live test must establish essential input/network/display. Stop on disk/BitLocker/EFI ambiguity rather than force installation.
