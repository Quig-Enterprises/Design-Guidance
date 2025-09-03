```markdown
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
 * Author:            Your Name or Quig Enterprises
 * Author URI:        https://github.com/Quig-Enterprises
 * License:           GPL-2.0-or-later
 * License URI:       https://www.gnu.org/licenses/gpl-2.0.html
 * Text Domain:       cxq-my-awesome-plugin
 * Domain Path:       /languages
 */

// If this file is called directly, abort.
if ( ! defined( 'WPINC' ) ) {
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
if ( ! defined( 'WP_UNINSTALL_PLUGIN' ) ) {
    exit;
}

// Example: Delete a custom option from the wp_options table.
delete_option( 'cxq_my_awesome_plugin_settings' );

// Example: Drop a custom database table.
global $wpdb;
$wpdb->query( "DROP TABLE IF EXISTS {$wpdb->prefix}cxq_custom_data" );
```
```