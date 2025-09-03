# Overall Design Strategy

This document outlines the high-level architectural principles that guide our development process at CxQ. The goal is to build software that is robust, scalable, and easy to maintain.

## 1. Follow Current Best Practices

Technology is always evolving. As developers, we are expected to stay informed about the current best practices for the languages and frameworks we use. This includes, but is not limited to:

*   **Security:** Sanitize all inputs, escape all outputs, and use nonces where appropriate (especially in a WordPress context).
*   **Performance:** Write efficient code and queries. Avoid loading unnecessary assets.
*   **Modern Language Features:** Utilize modern features of PHP (e.g., strict types, modern array syntax) and JavaScript (ES6+ features) to write cleaner and more robust code.

## 2. Object-Oriented Programming (OOP) by Default

We will use an Object-Oriented approach for designing our software. OOP helps us create modular, reusable, and maintainable code.

*   **When to Use OOP:** Any functionality that encapsulates data and behavior should be built as a class. This is especially true for design aspects that could be reused, either within the same plugin or across different plugins.
    *   *Good candidates for classes:* A settings manager, an API client, a data logger, a shortcode handler.
    *   *Poor candidates for classes:* A simple collection of unrelated helper functions (though these could be part of a static helper class).

*   **Principles to Follow:**
    *   **Single Responsibility Principle:** Each class should have only one reason to change.
    *   **Don't Repeat Yourself (DRY):** Abstract reusable logic into methods or parent classes.

## 3. Prioritize Reusability: Check the Catalog First

Before writing any new code, especially for common tasks, you must **always check the [Available Libraries catalog](./AVAILABLE_LIBRARIES.md)**.

*   **Why?** Reusing existing, tested code is faster and less error-prone than building from scratch. It ensures consistency across our projects.
*   **What if a library doesn't exist?** If you identify a need for a new reusable component (e.g., a new API integration, a complex UI element), propose it for inclusion as a new standalone library. This allows others to benefit from your work.

By following these strategic principles, we can build a cohesive and powerful ecosystem of tools.
