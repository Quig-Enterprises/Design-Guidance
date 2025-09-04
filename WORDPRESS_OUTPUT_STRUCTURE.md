# Output Structure for WordPress Plugins

To ensure our WordPress plugins are easy to install, distribute, and maintain, they must be packaged in a specific way. The standard is to create a single `.zip` file that can be uploaded directly through the WordPress admin dashboard (`Plugins > Add New > Upload Plugin`).

This document outlines the required file and folder structure.

## 1. The Root Directory and Zip File

The final output must be a `.zip` file named after the plugin's slug (e.g., `cxq-auditor.zip`). When unzipped, this file should create a single root directory with the same name (e.g., `/cxq-auditor`).

**Correct Structure:**
```
cxq-auditor.zip
└── /cxq-auditor
    ├── cxq-auditor.php
    └── ... (other files and folders)
```

**Incorrect Structure (Files in root of zip):**
```
cxq-auditor.zip
├── cxq-auditor.php
├── uninstall.php
└── ... (other files and folders)
```

## 2. Standard Folder Structure

A well-organized folder structure is essential for keeping your plugin's files manageable and separating concerns. We will use the following standard structure:

```
/plugin-slug/
|
|-- plugin-slug.php         # Main plugin file with the header.
|-- uninstall.php           # Code to run on plugin DELETION.
|-- README.txt              # WordPress.org standard readme file.
|
|-- /assets/                # For all publicly accessible, front-end assets.
|   |-- /css/               # Public-facing stylesheets.
|   |-- /js/                # Public-facing JavaScript.
|   |-- /images/            # Public-facing images.
|
|-- /admin/                 # For all admin-area specific assets and functionality.
|   |-- /css/               # Admin-area stylesheets.
|   |-- /js/                # Admin-area JavaScript.
|   |-- /images/            # Admin-area images.
|   |-- admin-page-view.php # Example admin page template.
|
|-- /includes/              # For all backend PHP files (classes, functions).
|   |-- class-plugin-name-activator.php
|   |-- class-plugin-name-deactivator.php
|   |-- class-plugin-name-main.php
|
|-- /languages/             # For translation files (.pot, .po, .mo).
|   `-- plugin-slug.pot
|
`-- /vendor/                # Composer dependencies (if any).
```
**Note on `README.txt`:** The `README.txt` file, if created for WordPress.org compatibility, should also list `Quig Enterprises` as the author/contributor to maintain consistency with the main plugin header.

## 3. The Main Plugin File (`plugin-slug.php`)

This is the entry point for your plugin. It must contain the standard WordPress plugin header comment at the very top. This header is critical as it's how WordPress identifies the plugin and its metadata.

**Header Template:**
```php
<?php
/**
 * Plugin Name:       CxQ My Awesome Plugin
 * Plugin URI:        https://github.com/Quig-Enterprises/cxq-my-awesome-plugin
 * Description:       A brief and clear description of what this plugin does.
 * Version:           1.0.0
 * Author:            Quig Enterprises
 * Author URI:        https://quigs.com
 * License:           GPL-2.0-or-later
 * License URI:       https://www.gnu.org/licenses/gpl-2.0.html
 * Text Domain:       cxq-my-awesome-plugin
 * Domain Path:       /languages
 */

// If this file is called directly, abort.
if ( ! defined( 'WPINC'  ) ) {
    die;
}

// Define plugin version constant.
define( 'CXQ_MY_AWESOME_PLUGIN_VERSION', '1.0.0' );

// Include the main plugin class.
require_once plugin_dir_path( __FILE__ ) . 'includes/class-plugin-name-main.php';

// Function to start the plugin.
function run_cxq_my_awesome_plugin() {
    $plugin = new CxQ_My_Awesome_Plugin_Main();
    $plugin->run();
}

run_cxq_my_awesome_plugin();
```

## 4. The `uninstall.php` File

This file is used to clean up any data your plugin has created **when a user deletes the plugin** via the WordPress dashboard. This is crucial for good plugin citizenship.

*   **Purpose:** Delete custom database tables, remove options from the `wp_options` table, and clean up any other artifacts.
*   **Note:** This script is only executed on deletion, not on deactivation.

**Template for `uninstall.php`:**
```php
<?php
/**
 * Fired when the plugin is uninstalled.
 *
 * @link       https://github.com/Quig-Enterprises
 * @since      1.0.0
 *
 * @package    Cxq_My_Awesome_Plugin
 */

// If uninstall not called from WordPress, then exit.
if ( ! defined( 'WP_UNINSTALL_PLUGIN'  ) ) {
    exit;
}

// Example: Delete a custom option from the wp_options table.
delete_option( 'cxq_my_awesome_plugin_settings' );

// Example: Drop a custom database table.
global $wpdb;
$wpdb->query( "DROP TABLE IF EXISTS {$wpdb->prefix}cxq_custom_data" );
```

## 5. Packaging and Distribution Rules

This section outlines the final rules for creating the distributable `.zip` file for a plugin. Adhering to these rules ensures that every plugin we deliver is professional, versioned correctly, and error-free upon installation.

### 5.1. Zip File Naming Convention

When generating the final `.zip` file, the filename **must** include a version number that corresponds to the version in the plugin's header and changelog.

*   **Correct Format:** `plugin-slug-MAJOR.MINOR.PATCH.zip`
    *   *Example:* `cxq-auditor-1.0.0.zip`
    *   *Example:* `cxq-membership-2.1.3.zip`

*   **Incorrect Formats:** Do not use descriptive or non-standard suffixes.
    *   *Avoid:* `cxq-auditor-latest.zip`
    *   *Avoid:* `cxq-auditor-debug-fix.zip`

This practice ensures that every distributed file is a unique, identifiable artifact tied to a specific release.

### 5.2. Pre-Packaging Verification Checklist

Before generating the `.zip` file, you **must** verify that the plugin is in a runnable state. A plugin distributed in a zip file must activate and run without generating fatal PHP errors.

*   **Ensure All Files Exist:** Every file that is referenced via `require`, `include`, `require_once`, or `include_once` must exist in the packaged directory. If a file is under development, it must exist as a placeholder with proper PHP comments explaining its purpose.

*   **Ensure All Functions/Methods Exist:** Every function or class method that is called must be defined. If a function's logic is not yet complete, it must exist as a valid placeholder to prevent "Call to undefined function/method" errors.

    ```php
    <?php
    /**
     * Processes the uploaded data.
     *
     * @todo Implement the full logic for data processing in a future iteration.
     * @return bool Always returns true for now.
     */
    function cxq_auditor_process_data( $data ) {
        // Placeholder: Full logic to be implemented later.
        // For now, we return true to prevent fatal errors in the call stack.
        return true;
    }
    ```

*   **Syntax Check:** The entire plugin codebase must be free of PHP syntax errors.

Following this checklist guarantees a professional user experience and prevents site-breaking errors upon plugin activation.
