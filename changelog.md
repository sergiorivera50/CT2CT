# Changelog
## Unreleased
- **Desktop version** for querying the model and get a complete reconstructed scan.

## 0.1.0-alpha - 2020-01-22
### Added
- **Save** and **Load** CT2CT models into/from a single file.
- This changelog.

### Changed
- **Performance** has substantially increased.
- CT2CT.ipynb is now easier to understand with a **step-by-step** explanation of each cell.
- **Images don't have to be stored in google drive anymore**.
- No longer necessary to download default scan as it is retrieved automatically via code.
- **Merging images** for input has been improved with a different formula (no more pixel multiplication).
- Images are now **single channel (grey scale)** rather than multi-channel (colored) as it improves training.
- Documentation has also been improved.

### Removed
- Storing generated input/target as well as raw scan images in google drive. Now they are stored in code.
- Therefore, folders /inputIMG, /outputIMG and /rawIMG have been removed.
- Support for complete scan prediction has also been removed but it will be added when the querying desktop version is ready.
- Therefore, folders /generatedScan, /results and /scan_dataset have been removed.
