# Changelog

## [0.1.12] - 2026-08-13

### Changed
- 安装童视锁后不再设置缺省初始密码：应用首次运行直接进入二维码界面，未设置口令时开机/亮屏/桌面拉起直接进入真实桌面。安装流程不再发送初始密码广播，Step 2 只安装 APK 并校验包存在。

## [0.1.11] - 2026-08-07

### Changed
- 版本维护发布：同步安装助手版本号与打包元数据（无功能变更）。

## [0.1.10] - 2026-07-26

### Fixed
- 执行日志、默认桌面诊断和后端错误文本统一使用英文，不再跟随界面语言切换。
- 设备所有者设置失败时保持设备所有者模式的失败语义，不再错误降级为可被普通卸载的活跃管理员。

## [0.1.9] - 2026-07-25

### Fixed
- 防卸载（设备所有者）设置失败时不再降级为 `dpm set-active-admin`。活跃管理员仍可被普通卸载，假报"防卸载已开启"会误导用户、毫无意义。
- `set-device-owner` 失败时 UI 仅提示"当前电视系统受限，防卸载设置失败。设备不支持设备所有者…"；原始 ADB 异常堆栈只记录到日志面板，不再暴露给用户。
- 修正 `dumpsys device_policy` 的状态识别语义：仅当出现真正的 `Device Owner` 段才视为防卸载已开启，避免把仅活跃管理员误判为已启用防卸载。

## [0.1.8] - 2026-07-25

### Fixed
- Detect KidTVLock device-admin/owner status via `dumpsys device_policy` instead of `dpm list-owners`, which some customized ROMs (e.g. Hisense VIDAA) do not implement.
- Fall back to `dpm set-active-admin` when `set-device-owner` fails on customized ROMs, so the防卸载 button no longer aborts with a raw stack trace.
- Keep the original ADB error stack in the log panel only; surface a concise "当前电视系统受限，防卸载设置失败" message in the UI.

## [0.1.7] - 2026-07-25

### Fixed
- Pin all device-specific ADB commands to the TV selected during connection, preventing offline emulators or other transports from causing `more than one device/emulator` errors.
- Retry the initial password broadcast once when a TV ROM returns `result=0`, while preserving the raw results if the retry is not confirmed.

## [0.1.6] - 2026-07-02

### Added
- Enable a KidTVLock accessibility HOME fallback when a TV ROM keeps another default HOME such as `FallbackHome` despite accepting the default-home command.

### Fixed
- Verify expected release assets before dispatching release-site synchronization.

## [0.1.5] - 2026-07-02

### Fixed
- Package the Windows ADB runtime DLLs with the installer so bundled `adb.exe` starts without requiring users to copy `AdbWinApi.dll` manually.
- Fail Windows builds early when required ADB runtime DLLs are missing.

## [0.1.4] - 2026-07-01

### Fixed
- Include stopped packages when sending the initial password broadcast so freshly installed KidTVLock builds can receive the setup command on stricter TV ROMs such as fengOS.

## [0.1.3] - 2026-06-26

### Added
- Hold Shift and click the install button to choose a local APK file and install it directly to the TV, bypassing the remote download. Useful for installing debug builds or older versions.
- Add `tauri-plugin-dialog` for native file picker support.

### Changed
- Improve default home diagnostics: log HOME list and disabled packages before and after setup, and provide more specific failure messages when the TV ROM rejects the default home change despite KidTVLock being a candidate.
- Show diagnostic log details (HOME list, disabled packages) in production builds for better support.

### Fixed
- Shift+click local APK install no longer triggers an unnecessary remote version check before opening the file dialog.

## [0.1.2] - 2026-06-21

### Changed
- Reduce installer window size from 1440x980 to 1280x820 for better small screen compatibility.
- Optimize UI layout spacing and padding to fit the smaller window.
- Update app icons with refined visual appearance.

### Fixed
- Add Windows arm64 installer build support.
- Publish tools packages to release repository during sync.
- Sync supported installer assets correctly.

## [0.1.1] - 2026-06-20

### Changed
- Publish the desktop installer release flow for both `terranc/KidTVLock-Tools` and the shared `terranc/KidTVLock` release repository.
- Refresh release sync skill copies and manifests across supported agent surfaces.

### Fixed
- Keep release-note fallback generation from failing when the latest tag is not yet resolvable during sync.
