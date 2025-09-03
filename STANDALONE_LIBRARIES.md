# Standalone Libraries: Creation and Usage

A core principle of our design strategy is reusability. To facilitate this, we will create and maintain a set of standalone libraries that can be shared across multiple CxQ plugins. This document provides the guidance for creating, versioning, and using these libraries.

## 1. What Qualifies as a Library?

Not all reusable code should be a library. A standalone library should be:

*   **Framework Agnostic (when possible):** It should have minimal dependencies on a specific framework like WordPress. If it must be framework-dependent, its purpose should be to abstract a complex framework feature (e.g., a `CxQ_WP_Settings_API_Wrapper`).
*   **Single Responsibility:** The library should do one thing and do it well (e.g., logging, making API calls, handling data sanitization).
*   **Well-Defined API:** It must have a clear, public-facing set of methods and properties for interaction. Internal logic should be kept private or protected.
*   **Independently Versioned:** It must follow our [Revisioning (SemVer)](./REVISIONING.md) guidelines and have its own `CHANGELOG.md`.

## 2. Library Naming and Structure

*   **Repository Name:** The GitHub repository name should be `kebab-case` and prefixed with `cxq-`.
    *   *Example:* `cxq-logger`, `cxq-api-client`

*   **PHP Namespace:** All classes within the library must belong to a `CxQ` root namespace, followed by a `PascalCase` version of the library name.
    *   *Example:* `CxQ\Logger`, `CxQ\ApiClient`

*   **File Structure:** Libraries should be structured to be compatible with a PSR-4 autoloader (like the one provided by Composer).
    ```
    /cxq-logger/
    |
    |-- /src/
    |   |-- Logger.php          # Contains the CxQ\Logger\Logger class
    |   `-- LogHandler.php    # Contains the CxQ\Logger\LogHandler class
    |
    |-- composer.json         # Defines dependencies and autoloading.
    |-- README.md             # Explains what the library is and how to use it.
    `-- CHANGELOG.md          # Follows our revisioning guidelines.
    ```

*   **Status:** Each library must have a defined status indicating its current state of development and availability. The possible statuses are:
    *   `Standalone`: The library is in its own repository and managed via Composer.
    *   `Embedded`: The library is currently developed/maintained within a larger plugin.
    *   `In Development`: The library is being actively built and is not yet stable.
    *   `Deprecated`: The library is no longer recommended for use and will be removed in the future.

## 3. Encapsulation: Namespaces vs. Prefixes

**Libraries must use their defined PHP namespace (e.g., `CxQ\Logger`) for all classes. Unlike plugins, libraries should avoid using global function prefixes (e.g., `cxq_logger_`) and should encapsulate all functionality within classes.** This reinforces our Object-Oriented and reusability principles.

## 4. Creating a New Library (The Process)

1.  **Identify the Need:** You recognize a piece of functionality that is, or could be, used in more than one plugin.
2.  **Check the Catalog:** First, you **must** check the [Available Libraries Catalog](./AVAILABLE_LIBRARIES.md) to ensure a similar library doesn't already exist.
3.  **Propose the Library:** Open an issue in the `Design-Guidance` repository outlining the purpose of the new library, its proposed API, and why it's needed.
4.  **Approval:** The proposal will be reviewed. Once approved, a new repository will be created under the `Quig-Enterprises` organization.
5.  **Development:** Build the library following all design guidance (OOP, Naming, Versioning). It must be fully documented with a `README.md`.
6.  **Add to Catalog:** Once the library is stable (`1.0.0`), add it to the `AVAILABLE_LIBRARIES.md` catalog so others can find and use it.

## 5. Using Libraries in a Plugin

We will use **Composer** as the standard dependency manager for including libraries in our plugins.

*   Each plugin that consumes a library will have its own `composer.json` file.
*   The library will be listed as a requirement.
*   The `/vendor` directory (containing the library code) will be included in the plugin's final `.zip` file.

This approach ensures that each plugin gets the correct version of a library and avoids conflicts.
