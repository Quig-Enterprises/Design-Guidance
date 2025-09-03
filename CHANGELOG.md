# Changelog

All notable changes to the Design Guidance documents will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/ ),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html ).

## [Unreleased]

## [1.2.0] - 2025-09-03

### Changed
- **Major Change:** The `AVAILABLE_LIBRARIES.md` catalog has been removed from this repository. The canonical source of truth for the library list is now the `README.md` file within the `cxq-libs` monorepo.
- `README.md` has been updated to direct developers to the `cxq-libs` repository for the library catalog.
- Guidance version updated to `1.2.0`.

## [1.1.0] - 2025-09-03

### Added
- New `AUTHENTICATION.md` document with detailed instructions for accessing the private monorepo via Composer using a GitHub Personal Access Token.

### Changed
- Major Strategy Update: All shared libraries are now managed in a private monorepo (`cxq-libs`).
- `STANDALONE_LIBRARIES.md` has been updated to reflect the new monorepo folder structure (`/packages`).
- `AVAILABLE_LIBRARIES.md` was updated so all libraries were marked with `Status: Standalone`.
- `README.md` was updated to link to the new `AUTHENTICATION.md` guide and the guidance version was updated to `1.1.0`.

## [1.0.0] - 2025-09-03

### Added
- Initial creation of all core guidance documents.
- Population of `AVAILABLE_LIBRARIES.md` with the first four core libraries.
- `CHANGELOG.md` to track changes to the guidance itself.

### Changed
- Updated `WORDPRESS_OUTPUT_STRUCTURE.md` to set the standard `Author` to "Quig Enterprises" and `Author URI` to "https://quigs.com".
- Performed a full cross-referencing analysis to improve consistency.
- Clarified in `STANDALONE_LIBRARIES.md` that libraries must use PHP namespaces exclusively for encapsulation.
- Formalized a `Status` field for all entries in `AVAILABLE_LIBRARIES.md`.
- Added a note to `WORDPRESS_OUTPUT_STRUCTURE.md` to ensure `README.txt` author info is consistent.
- Added a version number to the main `README.md`.
