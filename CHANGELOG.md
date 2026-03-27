> `Changelog:`
> - All significant changes to this project will be documented here.
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
---