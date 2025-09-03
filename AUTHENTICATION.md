# Authentication for Private Repositories

To use any of the shared CxQ libraries, you must first configure your local environment to authenticate with the private `cxq-libs` GitHub repository. This is a required, one-time setup step.

The recommended and most secure method is to use a **Fine-grained GitHub Personal Access Token (PAT)**.

## Step 1: Create a Fine-Grained Personal Access Token

This token acts as a secure, revocable password that grants Composer access.

1.  **Navigate to GitHub:** Go to `Settings` > `Developer settings` > `Personal access tokens` > `Fine-grained tokens`.
2.  **Generate a new token:**
    *   **Token name:** Give it a descriptive name (e.g., `manus-composer-access`).
    *   **Expiration:** Set an expiration date (e.g., 90 days). This is a critical security practice.
    *   **Repository access:** Select **"Only select repositories"** and choose the `Quig-Enterprises/cxq-libs` repository.
    *   **Permissions:** In the "Repository permissions" section, find **"Contents"** and set its access to **`Read-only`**. This is the minimum required permission and the most secure option.
3.  **Generate and Copy Token:** Click "Generate token" and immediately copy the token string (`github_pat_...`). **You will not see it again.**

## Step 2: Configure Your Plugin Project

In the root directory of the plugin you are developing, you need to tell Composer where to find the libraries and how to authenticate.

1.  **Update `composer.json`:** Add the private repository to your plugin's `composer.json` file.

    ```json
    {
        "name": "quig-enterprises/my-new-plugin",
        "repositories": [
            {
                "type": "vcs",
                "url": "https://github.com/Quig-Enterprises/cxq-libs.git"
            }
        ],
        "require": {
            "quig-enterprises/cxq-util-data-logger": "dev-main"
        }
    }
    ```

2.  **Create `auth.json`:** In the **same directory** as your `composer.json`, create a new file named `auth.json`. This file will store your secret token.

    ```json
    {
        "github-oauth": {
            "github.com": "github_pat_YourPastedPersonalAccessTokenHere"
        }
    }
    ```
    *Replace `github_pat_...` with the actual token you copied.*

3.  **CRITICAL: Add `auth.json` to `.gitignore`**
    To prevent your secret token from ever being committed to version control, add `auth.json` to your project's `.gitignore` file.

    ```
    # .gitignore
    /vendor
    composer.lock
    auth.json
    ```

## Step 3: Install Dependencies

You are now set up. Run `composer install` or `composer update` in your plugin's directory. Composer will automatically use the token from `auth.json` to securely access the `cxq-libs` repository and download the required packages.
