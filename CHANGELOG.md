> `Changelog:`
> - All significant changes to this project will be documented here.
---

> [5.0.0]
>
> - Added `SELF_PID` filter to shell deprioritization loop in `tweaks` and `univ` to prevent the script from deprioritizing itself.
> - Added a guard at the top of `customize.sh` to abort installation immediately if not running through Axeron/AxManager.
> - Added `uname -m` fallback in `customize.sh` arch detection for when `getprop ro.product.cpu.abi` returns nothing.
> - Added `aarch64` and `armv7l` to arch detection case pattern in `customize.sh` for `uname -m` compatibility.
> - Added `dev.axora.manager` package detection in `customize.sh` `check_axeron_requirement` alongside `frb.axeron.manager`.
> - Added `sha512`, `sha384`, `sha256`, and `sha224` hash algorithm support in `verify.sh` `extract()` alongside `md5` and `sha1`.
> - Added `author` check against `@illumi` in `verify.sh` `verify_module_id` alongside the existing `id` and `name` checks.
> - Added `ui_print` warning in `customize.sh` when device architecture is unsupported by `vmtouch`.
> - Added prop backup to `.props_backup` in `post-fs-data.sh` before modifying any debug properties.
> - Added `show_rotation_suggestions` (secure) and `enable_rotation_button` (system) settings in `service.sh` to hide the rotation suggestion button.
> - Added settings backup to `.settings_backup` in `service.sh` before modifying any global, secure, or system settings.
> - Added `device_config` backup to `.device_config_backup` in `univ` before modifying any device_config flags.
> - Added restore logic in `uninstall.sh` for `.props_backup`, `.settings_backup`, and `.device_config_backup`, deleting props and keys that had no original value, with fallback to delete if backup file is absent.
> - Added `net.ipv4.tcp_mtu_probing=1` in `tweaks` to prevent connection drops on networks with small MTU.
> - Added `net.ipv4.ip_local_port_range=1024 65535` in `tweaks` to expand available local ports.
> - Added `net.ipv4.tcp_rmem` and `net.ipv4.tcp_wmem` tuning in `tweaks` for higher per-socket TCP throughput.
> - Added `net.ipv4.tcp_rmem`, `net.ipv4.tcp_wmem`, `net.ipv4.tcp_mtu_probing`, `net.ipv4.ip_local_port_range`, and the zram compression algorithm to backup in `tweaks` for proper restore on uninstall.
> - Added 50MB size filter for `base.apk` pre-load in `tweaks` and `univ` to prevent excessive RAM usage on devices with many apps.
> - Added zram compression algorithm tuning to `lz4` in `tweaks` for better swap performance.
> - Added `add_random=0` and `rq_affinity=2` to I/O scheduler tuning in `tweaks` for reduced overhead and better CPU cache locality.
> - Added `debug.egl.traceGpuCompletion=0` in `post-fs-data.sh` to disable GPU completion tracing overhead.
> - Added `debug.sf.enable_gl_backpressure=0` in `post-fs-data.sh` to prevent frame stalls in SurfaceFlinger.
> - Added `debug.sf.early_phase_offset_ns` and `debug.sf.early_app_phase_offset_ns` in `post-fs-data.sh` for lower render thread latency.
> - Changed `uninstall.sh` case pattern from hardcoded `SEKOIIRE` to `$ID`.
> - Changed `.tweaks_backup` location from `$AXERONDIR` to `$AXMPATH` in `tweaks` and `uninstall.sh` for better plugin isolation.
> - Changed `customize.sh` `check_axeron_requirement` strings fallback filter to include `axora` keyword.
> - Changed `customize.sh` `check_axeron_requirement` to use a `for entry in "pkg:label"` loop pattern instead of `if-elif-else`, consistent with AAPT Multiarch's `detect_root_all` style.
> - Changed `customize.sh` root detection to use `$USER = "root"` directly instead of `$IS_ROOTED`/`$LOGNAME`/`$CURRENT_USER`.
> - Changed `banner` written to `module.prop` by `customize.sh` from the local `assets/SEKOIIRE.jpg` to the hosted `SEKOIIRE.jpg` at the repository root.
> - Changed `customize.sh` to open the Telegram channel once after every install; previously it sat inside a hash-file loop that never ran, so it never opened.
> - Changed `service.sh` root detection to use `$USER` only, removing the redundant `$LOGNAME` check.
> - Changed `customize.sh` to reference plugin paths as literal `$AXERONDIR/plugins/$ID` instead of the `$AXMPATH`/`$AXMPROP` variables.
> - Changed `verify.sh` success message from `Verified Plugins` to `Verified Plugin`.
> - Changed `customize.sh` RAM label in `device_info` to a single `ram_label()` helper shared by total and available RAM; values from 1GB to 4.5GB now display as `4GB`, and values above 13000MB display as exact GB (`MB / 1024`), dropping the previous `2GB`, `3GB`, `16GB`, and `32GB` labels.
> - Changed `net.core.netdev_max_backlog` in `tweaks` from `10000` to `16384` and `net.core.somaxconn` from `4096` to `8192` for higher connection capacity.
> - Changed `drop_caches` position in `tweaks` to before vmtouch pre-load sequence to ensure a clean page cache state.
> - Changed I/O scheduler tuning in `tweaks` to cover UFS devices (`sda`, `sdb`, `sdc`) with dynamic scheduler detection (`none` → `mq-deadline` → `noop`).
> - Changed I/O backup in `tweaks` to cover `sda`, `sdb`, `sdc` and `add_random`, `rq_affinity` nodes.
> - Changed TCP congestion control selection in `tweaks` to include `bbr2` and `westwood`; removed `cubic` and `reno` fallbacks.
> - Changed CPU foreground affinity in `tweaks` to read dynamically from `/sys/devices/system/cpu/present` instead of hardcoded `0-7`.
> - Changed CPU min freq for both clusters in `tweaks` to lock dynamically to `cpuinfo_max_freq` for full performance mode.
> - Changed GPU `default_pwrlevel` in `tweaks` from `3` to `0` for correct maximum performance level on Adreno.
> - Changed GPU `min_freq` in `tweaks` to lock dynamically to `devfreq/max_freq` for full performance mode.
> - Changed I/O `read_ahead_kb` in `tweaks` from `512` to `256` for better balance between sequential read and RAM usage.
> - Changed lib64 pre-load size filter in `tweaks` from 5MB to 10MB to cover more system libraries.
> - Changed `description` in `module.prop` and `service.sh` to reflect the plugin's actual function.
> - Changed the separator in the `service.sh` `description` from `•` to `|`.
> - Fixed `debug.stagefright.fps` in `post-fs-data.sh` to dynamically detect prop type and set `false` or `0` accordingly.
> - Fixed `customize.sh` permission loop to use `find -print0` with `read -r -d ''` instead of unquoted command substitution, preventing issues with filenames containing spaces.
> - Fixed `customize.sh` thermal blocks 16a and 16c composing a double-slash destination path (`$AXMPATH//system/...`); block 16c also now skips process names that are not absolute paths instead of creating stray files in the plugin root.
> - Fixed `customize.sh` `set_permissions` deleting the just-extracted `vmtouch` binary before it could be renamed: the non-root branch removed `vmtouch-arm64` and the root branch removed `vmtouch-arm32`, so `univ` lost its `vmtouch` dependency on non-root arm64 installs and on 32-bit root installs.
> - Fixed `post-fs-data.sh` forcing `debug.hwui.renderer=skiavk` and `ro.hwui.use_vulkan=true`, which caused video color issues on apps with custom video decoders; both props are no longer set.
> - Fixed `verify.sh` `verify_module_id` comparing `id` and `name` without stripping carriage returns, which made verification fail for a `module.prop` saved with CRLF line endings.
> - Fixed `tweaks` I/O scheduler backup storing the whole `[active] other` list instead of the active scheduler name, which made the scheduler impossible to restore on uninstall.
> - Fixed `tweaks` and `univ` running `blkdiscard` on raw partitions, which could cause data loss; storage trim now uses `fstrim` only.
> - Fixed `tweaks` and `univ` calling `fstrim` on block devices instead of mount points, which made the per-partition trim a silent no-op.
> - Removed `assets/SEKOIIRE.jpg` from ZIP extraction in `customize.sh`.
> - Removed `$AXERONDIR/.method` from cleanup list in `uninstall.sh`.
> - Removed `get_app_label` function from `customize.sh`; logic merged directly into `check_axeron_requirement`.
> - Removed `AXMPATH` and `AXMPROP` variable declarations from `customize.sh`.
> - Removed `AXERON` active state and minimum version checks from `customize.sh` `check_axeron_requirement`.
> - Removed dead hash-file deletion loop in `customize.sh`; hash files are never extracted into `$AXMPATH`.
> - Removed `clean_path` sanitizing of the ZIP path in `verify.sh` `extract()`; the path comes from `$ZIPFILE` and is now used as given.
> - Removed redundant `rm -f "$AXTWEAKSBACKUP"` from `uninstall.sh`; file is already removed as part of `$AXMPATH` cleanup.
> - Removed `audioserver` from RT priority boost in `tweaks` to avoid conflicts with Android's own RT scheduling.
> - Removed `dalvik.vm.dexopt.thermal-cutoff` override from `tweaks`; it is already handled by `thermal`.
> - Removed MSM thermal driver disable block from `tweaks`; it is already handled by `thermal`.
---

> [3.0.0]
>
> - Added RAM-based adaptive `swappiness` tuning in `tweaks`.
> - Added TCP congestion control with `bbr`/`cubic` fallback in `tweaks`.
> - Added TCP optimization: `low_latency`, `tw_reuse`, `ecn`, `fin_timeout`, `keepalive`, `syn_retries` in `tweaks`.
> - Added UDP buffer tuning (`udp_rmem_min`, `udp_wmem_min`) in `tweaks`.
> - Added `net/core` optimization: `rmem`, `wmem`, `somaxconn`, `netdev_budget`, `optmem_max` in `tweaks`.
> - Added shell process priority tuning via `ionice` and `renice` in `tweaks` and `univ`.
> - Added `sync` and `drop_caches` after sysctl tuning in `tweaks`.
> - Added pre-load for `dalvik-cache` and system fonts via `vmtouch -t` in `tweaks`.
> - Added numbered comments across all scripts for consistency.
> - Changed vmtouch framework and lib64 from `-l` (lock) to `-t` (pre-load) to prevent RAM exhaustion.
> - Changed `.vm_backup` to `.tweaks_backup` covering all sysctl parameters (vm, net.ipv4, net.core, kernel).
> - Changed `uninstall.sh` to restore sysctl parameters from `.tweaks_backup` instead of hardcoded values.
> - Changed plugin notification from `univ` to `service.sh`.
> - Fixed `thermal` self-kill issue with `SELF_PID` filter in `/proc` loop.
> - Fixed `get_app_label` in `customize.sh` to use `aapt` directly instead of `$AAPT_BIN` variable, with `strings` as fallback.
> - Removed private DNS (Cloudflare) settings from `service.sh` and `uninstall.sh`.
---

> [2.0.0]
>
> - Added `system/bin/vmtouch` with multiarch support (arm64/arm32) for page cache locking.
> - Added CPU, GPU, DDR, I/O, VM, and kernel tuning in `tweaks`.
> - Added per-script notifications for `univ`, `tweaks`, and `thermal`.
> - Added storage optimization via FSTRIM and BLKDISCARD.
> - Added TCP, DNS, and WiFi network optimization.
> - Changed `THERMAL` and `TWEAKS` into `system/bin/` as `thermal`, `tweaks`, and added `univ` for universal tweaks.
> - Changed `.md5` checksum to `.sha1`.
> - Changed root detection from `id -u` to `$LOGNAME`/`$USER`.
> - Changed `service.sh` with proper root/non-root detection via `$LOGNAME`.
> - Changed `post-fs-data.sh` with additional debug and rendering props.
> - Changed license from GNU General Public License to Apache License 2.0.
> - Fixed thermal overlay creation in `customize.sh` to avoid `mkdir/rmdir` warnings.
> - Removed `action.sh`, `socs.json`, and `PROP`.
> - Removed broken Telegram redirect on install.
---

> [1.0.0]
>
> - Initial release.
---