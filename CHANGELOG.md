## 2026-01-23

### Fixed

- Corrected the focal length ($f_x, f_y$) calculation logic in `colmap-camera-intrinsics/README.md`. It is now properly defined using the FOV formula ($f = \frac{W}{2 \tan(FOV/2)}$) instead of being incorrectly attributed to half the resolution.

## 2026-01-16

### New Features

- Created `colmap-camera-intrinsics/` experiment documentation to evaluate manual camera intrinsics in COLMAP.
- Updated system specifications across all documentation to reflect Windows 11 as the host operating system.

## 2026-01-13

### New Features

- Initial documentation for the Gaussian Splatting overall workflow created under the `gaussian-splatting-overall-workflow/` directory.