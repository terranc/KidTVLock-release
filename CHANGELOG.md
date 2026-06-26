# Changelog

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
