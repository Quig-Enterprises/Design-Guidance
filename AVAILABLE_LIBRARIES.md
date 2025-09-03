# Available Libraries

This document serves as a catalog of shared, standalone libraries available for use across all CxQ plugins. Utilizing these pre-approved libraries helps to reduce code duplication, improve stability, and accelerate development.

**Before building new functionality, always check this list to see if a suitable library already exists.**

## How to Use a Library

Each library listed below includes instructions for installation (e.g., via Composer) and usage. All libraries follow our established [Revisioning](./REVISIONING.md) and [Naming Convention](./NAMING_CONVENTIONS.md) guidelines.

---

## Library Catalog

*(This section will be populated as libraries are created and approved.)*

### Example Library Entry:

*   **Library Name:** `cxq-logger`
*   **Version:** `1.2.0`
*   **Owner:** `@maintainer-github-handle`
*   **Description:** A standardized logging utility for writing events to the database and/or flat files. Supports different log levels (INFO, WARNING, ERROR).
*   **Repository:** `https://github.com/Quig-Enterprises/cxq-logger`
*   **Usage:**
    ```php
    // Include the autoloader
    require_once 'path/to/vendor/autoload.php';

    // Instantiate the logger
    $logger = new \CxQ\Logger\DatabaseLogger( );

    // Log a message
    $logger->log( 'User logged in successfully.', 'INFO', ['user_id' => 123] );
    ```

---
