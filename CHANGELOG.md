# Changelog

All notable changes to this project are documented in this file.

The format is based on Keep a Changelog and this project follows Semantic Versioning.

## [Unreleased]

### Added
- 

### Changed
- 

### Fixed
- 

### Removed
- 

## [1.1.57] - 2026-04-21

### Added
- Regression test to ensure `CNX-R###` barcodes remain unchanged after `init_db()` runs.

### Changed
- Updated startup migration behavior to preserve current router barcode format (`CNX-R###`).

### Fixed
- Fixed an issue where restarting the app could rewrite sequential router barcodes into scrambled `CNX-XXXXXX` values.

## [1.1.56] - 2026-04-20

### Added
- Inventory page pagination with total count display.
- Pagination controls: Home, Previous, Next, rows-per-page (50/100), and go-to-page input.

### Changed
- Inventory list column order moved Connectivity Type/Version and Source after Barcode.
- Inventory list default ordering changed to barcode descending.

### Fixed
- Improved filtering + pagination behavior by preserving query parameters across navigation.

---

## Release Entry Template

Copy this block for the next version and fill it:

## [x.y.z] - YYYY-MM-DD

### Added
- 

### Changed
- 

### Fixed
- 

### Removed
- 
