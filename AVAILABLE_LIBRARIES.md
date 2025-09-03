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
*   **Note:** This library is currently being developed and maintained within the CxQ Membership Plugin.

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
*   **Note:** This library is currently being developed and maintained within the CxQ Membership Plugin.

### CxQ Notification Engine

*   **Composer Name:** `quig-enterprises/cxq-util-notification-engine`
*   **Purpose:** A powerful, rule-based engine for sending automated, time-based email notifications related to any date-driven post type.
*   **Core Functionality:**
    *   Creates a `cxq_notification_rule` Custom Post Type, allowing admins to build unlimited, complex notification rules.
    *   Rules are configured with "IF" conditions (e.g., check `cxq_credential` posts where `expiration_date` is in the next 30 days) and "THEN" actions (e.g., email the user and their manager).
    *   Manages its own WP-Cron jobs for daily, weekly, or monthly rule evaluation.
    *   Includes a "Dry Run" mode for testing rules without sending emails and a logging system (which uses the `CxQ Data Logger`) for auditing.
*   **Use Case:** Ideal for sending expiration reminders, pre-event notifications, subscription warnings, or any other date-based automated communication.
*   **Note:** This library is currently being developed and maintained within the CxQ Membership Plugin.

### CxQ Workflow Engine

*   **Composer Name:** `quig-enterprises/cxq-util-workflow-engine`
*   **Purpose:** A generic framework for creating and managing linear, status-based workflows for any WordPress post type.
*   **Core Functionality:**
    *   Allows a host plugin to define a sequence of statuses for a CPT (e.g., `new` -> `in-progress` -> `complete`).
    *   Adds an admin meta box with an "Advance to Next Stage" button to the configured post type's editor screen.
    *   Can automatically change a post author's WordPress user role when the post reaches a specific status.
    *   Fires custom action hooks at each stage (`cxq_workflow_status_changed_{post_type}_{new_status}`), allowing for deep integration with the host plugin's business logic.
*   **Use Case:** Perfect for managing any multi-step process, such as candidate onboarding, article publishing pipelines, project management, or order fulfillment.
*   **Note:** This library is currently being developed and maintained within the CxQ Membership Plugin.

---
