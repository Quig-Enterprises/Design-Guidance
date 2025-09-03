### **Development Strategy: Creating Standalone Code Modules**

This document outlines the standard strategy for structuring and decoupling features within a WordPress plugin. The goal is to create modular, self-contained components. There are two primary paths to follow, depending on whether the new module is intended for immediate external use by other plugins.

---

#### **Path A: Standalone & Shareable (The "Composer Monorepo" Strategy)**

**Use this path when you are instructed to make a library "standalone and available for external use."** This prepares the library to be managed by Composer and eventually moved to its own repository.

**1. Naming Convention:**

*   **Namespace:** All classes within a shareable library must belong to a namespace prefixed with `CxQ\Util\`. For example, a library named "DataLogger" would use the namespace `CxQ\Util\DataLogger`.
*   **Class Names:** All class names must be prefixed with `CxQ_Util_`. This serves as a global, non-namespaced fallback to guarantee uniqueness. For example: `class CxQ_Util_DataLogger_Admin_Table`.

**2. Project Structure:**

The project will be organized as a monorepo. All shareable libraries must reside within a `packages/` directory.

```
/main-plugin/
|-- /packages/
|   |-- /new-library-name/
|   |   |-- /src/
|   |   |-- composer.json
|   |   |-- README.md
|-- /vendor/
|-- main-plugin.php
|-- composer.json
|-- .gitignore
```

**3. Composer Configuration:**

This setup uses Composer's `path` repositories to symlink the local library into the `vendor/` directory, enabling live development.

*   **Library's `composer.json` (`packages/new-library-name/composer.json`):**
    *   Define the library's unique name (e.g., `quig-enterprises/cxq-util-data-logger`).
    *   Define its PSR-4 autoloader configuration according to the namespace convention:
        ```json
        "autoload": {
            "psr-4": {
                "CxQ\\Util\\DataLogger\\": "src/"
            }
        }
        ```

*   **Main Plugin's `composer.json` (`main-plugin/composer.json`):**
    *   Add the new library to the `require` section with the `@dev` version constraint.
    *   Ensure the `repositories` section is configured to scan the `packages/` directory:
        ```json
        "repositories": [
            {
                "type": "path",
                "url": "packages/*",
                "options": {
                    "symlink": true
                }
            }
        ]
        ```

**4. Workflow:**

1.  After creating the files, run `composer install` in the main plugin's root.
2.  Develop the library's code directly within its `packages/new-library-name/` directory, adhering to the naming conventions.
3.  The main plugin must include the `vendor/autoload.php` file and can then use the library's classes.
4.  **Crucially, create a detailed `README.md`** with full integration instructions for the library, as it is intended for external use.

---

#### **Path B: Standalone & Private (The "Internal Module" Strategy)**

**Use this path when you are instructed to make a library "standalone but NOT available for external use (yet)."** This approach prioritizes code organization without the overhead of Composer dependency management for that specific module.

**1. Naming Convention:**

*   **Namespace:** All classes within a private module must belong to the main plugin's primary namespace.
*   **Class Names:** All class names must share the same unique prefix as the rest of the host plugin. The format is `CxQ_XXXX_`, where `XXXX` is a unique identifier for the host plugin (e.g., `CxQ_Membership_`). For example, a private module for handling imports within the "Membership" plugin would have a class named `CxQ_Membership_Import_Manager`.

**2. Project Structure:**

The module is still placed in its own directory for separation, but it is treated as a simple part of the main plugin.

```
/main-plugin/
|-- /includes/
|   |-- /modules/
|   |   |-- /new-module-name/
|   |   |   |-- /src/
|   |   |   |-- new-module-name.php  (The main loader file)
|-- main-plugin.php
|-- composer.json
```

**3. Autoloading Configuration:**

Instead of a `path` repository, you will add the module's directory directly to the main plugin's `composer.json` autoload section.

*   **Main Plugin's `composer.json` (`main-plugin/composer.json`):**
    *   Add a new PSR-4 namespace for the internal module, nested under the main plugin's namespace.
        ```json
        "autoload": {
            "psr-4": {
                "CxQ\\Membership\\": "includes/",
                "CxQ\\Membership\\Modules\\NewModuleName\\": "includes/modules/new-module-name/src/"
            }
        }
        ```
    *   After updating the `composer.json`, run `composer dump-autoload` to regenerate the autoloader.

**4. Workflow:**

1.  The main plugin file (`main-plugin.php`) is responsible for including the module's main loader file (`includes/modules/new-module-name/new-module-name.php`).
2.  This loader file is responsible for instantiating the module's classes.
3.  Since this module is not intended for external use, it does not need its own `composer.json` or a public-facing `README.md` with integration instructions. Its use is entirely controlled by the main plugin.