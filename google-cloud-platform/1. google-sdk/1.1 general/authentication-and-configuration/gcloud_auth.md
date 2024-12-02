File: [[gcloud_auth.md]]
Labels: #gcp #auth #config
Description: Commands to authenticate with GCP and configure your CLI (`gcloud auth`, `gcloud config`).
Related to: [[gcloud_projects.md]], [[gcloud_billing.md]]

###### **Log in with your Google Account**

```bash
gcloud auth login
```

- Opens a browser window for authentication.
- Useful for interacting with GCP from the CLI.

###### **List authenticated accounts**

```bash
gcloud auth list
```

- Displays the authenticated accounts on your system.
- Highlights the active account.

###### **Set an active account**

```bash
gcloud config set account user@google.com
```

Sets the active account used by `gcloud` commands.

###### **Application default authentication**

```bash
gcloud auth application-default login
```

- Used to authenticate applications that use GCP client libraries.
- Generates credentials at `~/.config/gcloud/application_default_credentials.json`.

**Note**: This method is primarily useful for development environments. In production, using service account credentials is recommended.

###### **Set credentials for applications**

Linux/MacOS:

```bash
export GOOGLE_APPLICATION_CREDENTIALS="~/.config/gcloud/application_default_credentials.json"

```

Windows (CMD):

```bash
set export GOOGLE_APPLICATION_CREDENTIALS="C:\Users\YourUser\.config\gcloud\application_default_credentials.json"
```

Windows (PowerShell):

```bash
$env:GOOGLE_APPLICATION_CREDENTIALS="C:\Users\YourUser\.config\gcloud\application_default_credentials.json"
```

##### **Revoke authentication**

For user accounts:

```bash
gcloud auth revoke user@google.com
```

Revokes access for a specific account.

Revoke all accounts:

```bash
gcloud auth revoke --all
```

###### **Manually obtain an access token**

```bash
gcloud auth print-access-token
```

- Generates a token you can use to make API requests directly.
- Useful for quick tests or debugging.

###### **Configuration profiles with `gcloud`**

Create a new configuration:

```bash
gcloud config configurations create new-config
```

###### **Switch between configurations:**

```bash
gcloud config configurations activate config-name
```

###### **List existing configurations:**

```bash
gcloud config configurations list
```

###### **Delete a configuration:**

```bash
gcloud config configurations delete config-name
```

##### **Related Links**

- [[gcloud_projects.md]]: Learn how to manage projects and accounts in GCP.
- [[gcloud_billing.md]]: Setup and manage billing accounts associated with your projects.
- [[gcloud_iam_roles.md]]: Information about roles and permissions in GCP.

---

##### **Notes**

- **Required permissions:** Ensure you have the necessary permissions to run authentication and configuration commands, such as `roles/iam.serviceAccountUser` or `roles/owner`.
- **Billing accounts:** Authentication credentials are required to work with paid resources associated with billing accounts.
- **Access tokens:** Tokens manually generated with `gcloud auth print-access-token` have a limited lifespan (usually 1 hour) and should not be used in production.
