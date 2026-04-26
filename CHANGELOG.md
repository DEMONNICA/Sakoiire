> Changelog:
> - All significant changes to this project will be documented here.
---

> [3.0.0]
>
> - Added RAM-based adaptive `swappiness` tuning in `tweaks`.
> - Added TCP congestion control with `bbr`/`cubic` fallback in `tweaks`.
> - Added TCP optimization: `low_latency`, `tw_reuse`, `ecn`, `fin_timeout`, `keepalive`, `syn_retries` in `tweaks`.
> - Added UDP buffer tuning (`udp_rmem_min`, `udp_wmem_min`) in `tweaks`.
> - Added `net/core` optimization: `rmem`, `wmem`, `somaxconn`, `netdev_budget`, `optmem_max` in `tweaks`.
> - Added shell process priority tuning via `ionice` and `renice` in `tweaks` and `univ`.
> - Added `sync` and `drop_caches` after tuning in `tweaks`.
> - Added pre-load for `dalvik-cache` and system fonts via `vmtouch -t` in `tweaks`.
> - Changed vmtouch framework and lib64 from `-l` (lock) to `-t` (pre-load) to prevent RAM exhaustion.
> - Replaced `.vm_backup` with `.tweaks_backup` covering all sysctl parameters (vm, net.ipv4, net.core, kernel).
> - `uninstall.sh` now restores sysctl parameters from `.tweaks_backup` instead of hardcoded values.
> - Moved plugin notification from `univ` to `service.sh`.
> - Removed private DNS (Cloudflare) settings from `service.sh` and `uninstall.sh`.
> - Fixed `thermal` self-kill issue with `SELF_PID` filter in `/proc` loop.
> - Fixed `get_app_label` in `customize.sh` to use `aapt` directly instead of `$AAPT_BIN` variable, with `strings` as fallback.
> - Added numbered comments across all scripts for consistency.
---

> [2.0.0]
>
> - License changes.
> - Restructured `README.md` for better readability.
> - Overhauled `customize.sh` and `verify.sh` for improved reliability.
> - Removed `action.sh`, `socs.json`, and `PROP`.
> - Moved `THERMAL` and `TWEAKS` into `system/bin/` as `thermal`, `tweaks`, and added `univ` for universal tweaks.
> - Added `system/bin/vmtouch` with multiarch support (arm64/arm32) for page cache locking.
> - Replaced `.md5` checksum with `.sha1`.
> - Improved `service.sh` with proper root/non-root detection via `$LOGNAME`.
> - Improved `post-fs-data.sh` with additional debug and rendering props.
> - Replaced `id -u` check with `$LOGNAME`/`$USER` for root detection.
> - Fixed thermal overlay creation in `customize.sh` to avoid `mkdir/rmdir` warnings.
> - Added CPU, GPU, DDR, I/O, VM, and kernel tuning in `tweaks`.
> - Added per-script notifications for `univ`, `tweaks`, and `thermal`.
> - Added storage optimization via FSTRIM and BLKDISCARD.
> - Added TCP, DNS, and WiFi network optimization.
> - Removed broken Telegram redirect on install.
> - Misc improvements and fixes.
---

> [1.0.0]
>
> - Initial release.