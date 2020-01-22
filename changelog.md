# Changelog
## Unreleased
- Desktop version for querying the model and get a complete reconstructed scan.

## 0.1.0-alpha - 2020-01-22
### Added
- Save and Load CT2CT models into/from a single file.

### Changed
- Merging images for input has been improved with a different formula (no more pixel multiplication).
- Images are now single channel (grey scale) rather than multi-channel (colored) as it improves training.
- Code has been rewritten so it is easier to read.
- Notebook has a clear step-by-step guidance for training and testing.
- Documentation has also been improved.

### Removed
- Support for complete scan prediction as it will be added with the querying desktop version.
- Therefore, folders /generatedScan, /results and /scan_dataset have been removed.
