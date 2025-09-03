# Revisioning (Versioning)

A consistent versioning strategy is essential for managing releases, communicating the nature of changes to users, and maintaining a stable development workflow. We will use **Semantic Versioning (SemVer)** as our official versioning scheme for all plugins and libraries.

You can read the full SemVer specification at [https://semver.org/](https://semver.org/ ).

## 1. The SemVer Format: MAJOR.MINOR.PATCH

A version number is composed of three parts: `MAJOR.MINOR.PATCH`. We increment:

*   **`MAJOR`** when you make incompatible API changes. This indicates a significant change that may require users or other developers to modify their implementation.
    *   *Example:* Renaming a public function, changing the parameters of a widely used filter, or completely overhauling the plugin's architecture.

*   **`MINOR`** when you add new functionality in a backward-compatible manner. This signals that new features are available, but existing functionality remains unchanged.
    *   *Example:* Adding a new shortcode, introducing a new settings page, or creating a new widget.

*   **`PATCH`** when you make backward-compatible bug fixes. This is for correcting mistakes in the existing code.
    *   *Example:* Fixing a security vulnerability, correcting a PHP notice, or resolving a CSS alignment issue.

**Example Versioning Flow:**
*   `1.0.0` - Initial stable release.
*   `1.0.1` - A bug fix is released.
*   `1.1.0` - A new, backward-compatible feature is added.
*   `1.1.1` - Another bug fix for the new feature.
*   `1.1.2` - A security patch is released.
*   `2.0.0` - A major rewrite is released that breaks backward compatibility.

## 2. Maintaining a Changelog

Every plugin and library **must** include a `CHANGELOG.md` file in its root directory. This file provides a human-readable log of all notable changes made in each version.

The changelog should follow the format recommended by [Keep a Changelog](https://keepachangelog.com/en/1.0.0/ ).

**Changelog Best Practices:**

*   The file must be named `CHANGELOG.md`.
*   The top of the file should have an "Unreleased" section for ongoing changes.
*   Each version should have its own section with the release date.
*   Changes should be grouped under one of the following headings:
    *   `Added` for new features.
    *   `Changed` for changes in existing functionality.
    *   `Deprecated` for soon-to-be-removed features.
    *   `Removed` for now-removed features.
    *   `Fixed` for any bug fixes.
    *   `Security` in case of vulnerabilities.

### `CHANGELOG.md` Template

```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/ ),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html ).

## [Unreleased]

### Added
- 

## [1.1.0] - 2025-09-03

### Added
- New settings panel for customizing email notifications.
- [CxQ-123] Integration with the new CxQ Logging library.

### Fixed
- Resolved issue where non-admin users could see the settings link.

## [1.0.0] - 2025-08-15

### Added
- Initial release of the plugin.
- Core functionality for auditing user login events.
