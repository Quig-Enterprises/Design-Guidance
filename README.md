/# Manus AI Development Guidance: Best Practices for Building CxQ Plugins
/
/**Design Guidance Version:** 1.3.0
/
/Welcome to the central design guidance for all Manus AI chat sessions at CxQ. This repository contains a unified set of best practices for developing high-quality, consistent, and maintainable software.
/
/## Core Principles
/... (content remains the same) ...
/
/## Dependency Management Strategy
/
/CxQ plugins use a **Hybrid Dependency Management** approach that combines professional development practices with zero-configuration deployment:
/
/- **Development**: Full Composer dependency management with proper PSR-4 structure.
/- **Production**: All dependencies are bundled for immediate, zero-fuss WordPress deployment.
/- **Benefits**: This gives us a professional architecture while providing a user-friendly installation experience.
/
/See the **[Hybrid Dependency Management Guide](./HYBRID_DEPENDENCY_MANAGEMENT.md)** for complete implementation details.
/
/## Guidance Documents
/
/The following documents provide detailed instructions on specific aspects of our development process. Please familiarize yourself with each of them before starting a new project.
/
/*   **[Authentication](./AUTHENTICATION.md):** How to configure access to the private `cxq-libs` repository. **(Required First Step)**
/*   **[Hybrid Dependency Management](./HYBRID_DEPENDENCY_MANAGEMENT.md):** The official standard for managing dependencies in CxQ plugins.
/*   **[Overall Design Strategy](./DESIGN_STRATEGY.md):** High-level architectural principles.
/*   **[Naming Conventions](./NAMING_CONVENTIONS.md):** Rules for naming plugins, prefixes, variables, functions, and other code elements.
/*   **[Output Structure for WordPress Plugins](./WORDPRESS_OUTPUT_STRUCTURE.md):** Guidelines for packaging WordPress plugins for easy installation and distribution.
/*   **[Revisioning (Versioning)](./REVISIONING.md):** Our approach to software versioning using Semantic Versioning (SemVer).
/*   **[Standalone Libraries](./STANDALONE_LIBRARIES.md):** Guidance on creating, using, and contributing to the shared libraries within the `cxq-libs` monorepo.
/
/For a complete list and description of all available libraries, please see the `README.md` file in the **`cxq-libs`** repository.
