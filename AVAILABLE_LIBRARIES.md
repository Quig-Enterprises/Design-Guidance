# Available Libraries Catalog

This document serves as a catalog of shared, standalone libraries available for use across all CxQ plugins. Utilizing these pre-approved libraries helps to reduce code duplication, improve stability, and accelerate development.

**Before building new functionality, always check this list to see if a suitable library already exists.**

## How to Use a Library

Each library listed below includes its Composer name for easy installation. All libraries follow our established [Revisioning](./REVISIONING.md) and [Naming Convention](./NAMING_CONVENTIONS.md) guidelines. To use one, require it in your plugin's `composer.json` and run `composer install`.

---

## Library Catalog

### CxQ Data Logger

*   **Composer Name:** `quig-enterprises/cxq-util-data-logger`
*   **Purpose:** Provides a generic, configuration-driven system for creating and managing custom logs within the WordPress admin dashboard.
*   **Core Functionality:**
    *   Creates a master database table for storing log entries.
    *   Allows host plugins to register unique "log types" (e.g., `notification_log`, `api_error_log`).
    *   For each registered log type, it automatically generates a searchable, sortable, and filterable admin screen.
    *   Provides a simple, static `log()` method for writing events with contextual data stored as JSON.
*   **Use Case:** Ideal for auditing, debugging, or tracking any type of event within a plugin, such as API calls, user actions, or system errors.
*   **Note:** This library is currently being developed and maintained within the CxQ Membership Plugin. It will be migrated to its own repository upon reaching a stable version.

### CxQ Credential Manager

*   **Composer Name:** `quig-enterprises/cxq-util-credential-manager`
*   **Purpose:** A complete system for managing the entire lifecycle of user-submitted credentials, such as licenses or certifications.
*   **Core Functionality:**
    *   Creates a `cxq_credential` Custom Post Type.
    *   Handles secure file uploads, storing documents in a protected directory inaccessible from the web.
    *   Implements a "Verification Queue" where new uploads must be manually `Approved` or `Rejected` by an administrator.
    *   Features a pluggable architecture (`iCxQ_Verifier` interface) to allow for future automated verification methods (e.g., OCR).
    *   Provides front-end shortcodes for user upload forms and credential lists.
*   **Use Case:** Perfect for any site that needs to track and verify user qualifications, licenses, or certifications.
*   **Note:** This library is currently being developed and maintained within the CxQ Membership Plugin. It will be migrated to its own repository upon reaching a stable version.

### CxQ Notification Engine

*   **Composer Name:** `quig-enterprises/cxq-util-notification-engine`
*   **Purpose:** A powerful, rule-based engine for sending automated, time-based email notifications related to any date-driven post type.
*   **Core Functionality:**
    *   Creates a `cxq_notification_rule` Custom Post Type, allowing admins to build unlimited, complex notification rules.
    *   Rules are configured with "IF" conditions (e.g., check `cxq_credential` posts where `expiration_date` is in the next 30 days) and "THEN" actions (e.g., email the user and their manager).
    *   Manages its own WP-Cron jobs for daily, weekly, or monthly rule evaluation.
    *   Includes a "Dry Run" mode for testing rules without sending emails and a logging system (which uses the `CxQ Data Logger`) for auditing.
*   **Use Case:** Ideal for sending expiration reminders, pre-event notifications, subscription warnings, or any other date-based automated communication.
*   **Note:** This library is currently being developed and maintained within the CxQ Membership Plugin. It will be migrated to its own repository upon reaching a stable version.

### CxQ Workflow Engine

*   **Composer Name:** `quig-enterprises/cxq-util-workflow-engine`
*   **Purpose:** A generic framework for creating and managing linear, status-based workflows for any WordPress post type.
*   **Core Functionality:**
    *   Allows a host plugin to define a sequence of statuses for a CPT (e.g., `new` -> `in-progress` -> `complete`).
    *   Adds an admin meta box with an "Advance to Next Stage" button to the configured post type's editor screen.
    *   Can automatically change a post author's WordPress user role when the post reaches a specific status.
    *   Fires custom action hooks at each stage (`cxq_workflow_status_changed_{post_type}_{new_status}`), allowing for deep integration with the host plugin's business logic.
*   **Use Case:** Perfect for managing any multi-step process, such as candidate onboarding, article publishing pipelines, project management, or order fulfillment.
*   **Note:** This library is currently being developed and maintained within the CxQ Membership Plugin.It will be migrated to its own repository upon reaching a stable version.

---

### **CxQ Calendar Board (`quig-enterprises/cxq-calendar-board`)**

*   **Purpose:** Provides a complete, standalone, and provider-driven interactive calendar board for WordPress. It is designed to be the central UI for any plugin that needs to display and manage time-based events.
*   **Core Functionality:**
    *   Creates a full-screen, interactive calendar admin page using a modern JavaScript library (e.g., FullCalendar.io).
    *   Features a "provider-driven" architecture. The host plugin registers one or more data providers, and the library handles fetching, aggregating, and rendering all data sources on the calendar.
    *   Manages all front-end assets (JS/CSS) and the REST API endpoints required for the calendar to function.
    *   Designed to be completely agnostic of the data it displays; it knows nothing about "shifts" or "events," only about "data providers."
*   **Use Case:** Ideal for any plugin that requires a sophisticated scheduling UI, such as an event manager, a booking system, a project timeline tool, or a workforce scheduler.
*   **Status:** `In Development`.
*   **Note:** This library is currently being developed and maintained within the `cxq-scheduler` plugin's monorepo. It will be migrated to its own repository upon reaching a stable version

### **CxQ Time & Attendance Engine (`quig-enterprises/cxq-time-engine`)**

*   **Purpose:** A dedicated reporting engine for calculating and aggregating time-on-duty from a schedule-based Custom Post Type.
*   **Core Functionality:**
    *   Provides a `TimeCardEngine` class that can query shift data over any given date range.
    *   Supports multiple aggregation formats, allowing reports to be grouped by time period (Daily, Weekly, Monthly) or by personnel qualifications (e.g., hours covered by EMTs, hours covered by Drivers).
    *   Handles complex data queries and calculations on the back-end, returning a simple, structured data array ready for display.
    *   Designed to be integrated into a host plugin's UI, providing the core logic for time card and payroll reporting.
*   **Use Case:** Perfect for any scheduling plugin that needs to generate reports on workforce hours, payroll, or operational capacity based on skills.
*   **Status:** `In Development`.
*   **Note:** This library is currently being developed and maintained within the `cxq-scheduler` plugin's monorepo. It will be migrated to its own repository upon reaching a stable version
---

### CxQ Util Post Type Manager

*   **Composer Name:** `quig-enterprises/cxq-util-post-type-manager`
*   **Purpose:** A comprehensive WordPress custom post type management library that provides a fluent interface for defining and registering custom post types with automated label generation and sensible defaults.
*   **Core Functionality:**
    *   Fluent interface for clean, chainable post type configuration methods.
    *   Automatic generation of all 20+ WordPress post type labels from singular/plural names.
    *   Sensible defaults preconfigured for admin-only post types with common settings.
    *   Comprehensive input validation and detailed error handling with descriptive exceptions.
    *   Full customization support for overriding any WordPress post type argument.
    *   Built-in internationalization support with text domain configuration.
*   **Use Case:** Eliminates boilerplate code for custom post type creation across all plugins. Ideal for any plugin that needs to register multiple post types with consistent labeling and configuration patterns.
*   **Note:** This library is currently being developed and maintained within the CxQ Auditor Plugin. It will be migrated to its own repository upon reaching a stable version

### CxQ Util Meta Box Builder

*   **Composer Name:** `quig-enterprises/cxq-util-meta-box-builder`
*   **Purpose:** A comprehensive WordPress meta box builder library with fluent interface for creating admin UI components including dropdowns, multi-selects, sortable lists, and custom fields with automatic save handling.
*   **Core Functionality:**
    *   Fluent interface for defining meta boxes with various field types (text, textarea, dropdown, checkbox, etc.).
    *   Advanced UI components including searchable multi-select interfaces and drag-and-drop sortable lists.
    *   Automatic nonce security handling and data validation for all field types.
    *   Built-in CSS and JavaScript for enhanced user experience with sortable and dynamic interfaces.
    *   Conditional field display based on other field values.
    *   Automatic save/load handling with proper sanitization and capability checks.
*   **Use Case:** Rapid development of WordPress admin interfaces with consistent UX patterns. Perfect for plugins requiring complex admin forms, relationship management, or data entry interfaces.
*   **Note:** This library is currently being developed and maintained within the CxQ Auditor Plugin. It will be migrated to its own repository upon reaching a stable version

### CxQ Util Database Table Manager

*   **Composer Name:** `quig-enterprises/cxq-util-database-table-manager`
*   **Purpose:** A robust library for managing custom WordPress database tables with automated creation, migration handling, and performance optimization through proper indexing.
*   **Core Functionality:**
    *   Automated custom table creation with proper charset/collation handling using WordPress dbDelta.
    *   Index management for performance optimization with support for primary keys, foreign keys, and composite indexes.
    *   Version-aware migration system for safely updating table structures between plugin versions.
    *   Relationship table patterns for managing many-to-many associations between post types.
    *   Built-in validation and error handling for database operations.
    *   Support for complex table schemas with multiple data types and constraints.
*   **Use Case:** Essential for plugins requiring custom database tables for performance or complex data relationships that exceed WordPress meta capabilities. Ideal for audit trails, logging systems, or complex relational data.
*   **Note:** This library is currently being developed and maintained within the CxQ Auditor Plugin. It will be migrated to its own repository upon reaching a stable version

### CxQ Util Relationship Manager

*   **Composer Name:** `quig-enterprises/cxq-util-relationship-manager`
*   **Purpose:** A powerful library for creating and managing complex relationships between WordPress post types, including one-to-many, many-to-many, and hierarchical relationships with historical data preservation.
*   **Core Functionality:**
    *   Support for one-to-many relationships with dropdown selectors and admin column integration.
    *   Advanced many-to-many relationships using custom database tables with drag-and-drop ordering.
    *   Historical data snapshot functionality for preserving relationship data at specific points in time.
    *   Automatic meta box generation for relationship management with search and filter capabilities.
    *   Admin list table integration showing relationship data in custom columns.
    *   Comprehensive relationship validation and integrity checking.
*   **Use Case:** Perfect for plugins managing complex content relationships, audit systems requiring historical accuracy, or any application needing sophisticated data linking between different content types.
*   **Note:** This library is currently being developed and maintained within the CxQ Auditor Plugin. It will be migrated to its own repository upon reaching a stable version

### CxQ Util Admin Column Manager

*   **Composer Name:** `quig-enterprises/cxq-util-admin-column-manager`
*   **Purpose:** A streamlined library for adding and managing custom columns in WordPress admin list tables with support for sortable columns, custom data formatting, and relationship data display.
*   **Core Functionality:**
    *   Fluent interface for adding custom columns to any post type admin list.
    *   Support for sortable columns with custom sorting logic.
    *   Built-in data formatters for common data types (dates, relationships, status indicators).
    *   Automatic handling of relationship data display in columns.
    *   Responsive column management with priority-based hiding on smaller screens.
    *   Integration with WordPress list table pagination and filtering.
*   **Use Case:** Enhances WordPress admin user experience by providing relevant data at-a-glance in list views. Essential for plugins with custom post types that need to display relationship or meta data efficiently.
*   **Note:** This library is currently being developed and maintained within the CxQ Auditor Plugin. It will be migrated to its own repository upon reaching a stable version

### CxQ Util Asset Manager

*   **Composer Name:** `quig-enterprises/cxq-util-asset-manager`
*   **Purpose:** An optimized library for managing WordPress plugin assets (CSS, JavaScript) with conditional loading, dependency management, and performance optimization features.
*   **Core Functionality:**
    *   Conditional asset loading based on current admin screen, post type, or custom conditions.
    *   Automatic dependency management with support for WordPress core libraries and custom dependencies.
    *   Version control for cache busting with automatic file modification time detection.
    *   Separation of admin and frontend assets with appropriate loading contexts.
    *   Minification and concatenation support for production environments.
    *   Asset preloading and optimization for improved page load performance.
*   **Use Case:** Ensures optimal performance by loading only necessary assets when needed. Critical for plugins with complex admin interfaces or multiple frontend components.
*   **Note:** This library is currently being developed and maintained within the CxQ Auditor Plugin. It will be migrated to its own repository upon reaching a stable version

### CxQ Util Plugin Activator

*   **Composer Name:** `quig-enterprises/cxq-util-plugin-activator`
*   **Purpose:** A standardized library for managing WordPress plugin lifecycle events including activation, deactivation, and uninstallation with database setup and cleanup capabilities.
*   **Core Functionality:**
    *   Automated database table creation and initialization during plugin activation.
    *   Default option and setting initialization with validation.
    *   User capability and role setup for plugin-specific permissions.
    *   Version-aware migration handling for plugin updates.
    *   Clean deactivation with optional data preservation or removal.
    *   Comprehensive error handling and logging during lifecycle events.
*   **Use Case:** Provides consistent and reliable plugin installation and removal processes. Essential for plugins requiring database setup, custom user roles, or complex initialization procedures.
*   **Note:** This library is currently being developed and maintained within the CxQ Auditor Plugin. It will be migrated to its own repository upon reaching a stable version



