**File:** [[gcloud_auth.md]]
**Tags:** #gcp #auth #config
**Description:** Commands to authenticate to GCP and configure your CLI (`gcloud auth`, `gcloud config`).
**Related to:** [[gcloud_projects.md]], [[gcloud_billing.md]]

### **Sign in with your Google Account**

```bash
gcloud auth login
```

- Opens a browser window for authentication.
- Useful for interacting with GCP through the CLI.

### **List authenticated accounts**

```bash
gcloud auth list
```

- Displays the accounts authenticated on your system.
- Highlights the active account.

### **Set an active account**

```bash
gcloud config set account user@google.com
```

Changes the active account used by `gcloud` commands.

### **Default authentication for applications**

```bash
gcloud auth application-default login
```

- Used to authenticate applications that use GCP client libraries.
- Generates credentials at `~/.config/gcloud/application_default_credentials.json`.

**Note**: This method is mainly useful for development environments. For production, using service account credentials is recommended.

### **Set credentials for applications**

Linux/MacOS:

```bash
export GOOGLE_APPLICATION_CREDENTIALS="~/.config/gcloud/application_default_credentials.json"
```

Windows (CMD):

```bash
set GOOGLE_APPLICATION_CREDENTIALS="C:\Users\YourUsername\.config\gcloud\application_default_credentials.json"
```

Windows (PowerShell):

```bash
$env:GOOGLE_APPLICATION_CREDENTIALS="C:\Users\YourUsername\.config\gcloud\application_default_credentials.json"
```

### **Revoke authentication**

For user accounts:

```bash
gcloud auth revoke user@google.com
```

Revokes access for a specific account.

Revoke all accounts:

```bash
gcloud auth revoke --all
```

### **Manually obtain an access token**

```bash
gcloud auth print-access-token
```

- Generates a token for making API requests directly.
- Useful for quick tests or debugging.

### **Manage profiles with `gcloud`**

Create a new configuration:

```bash
gcloud config configurations create new-config
```

### **Switch between configurations:**

```bash
gcloud config configurations activate config-name
```

### **List existing configurations:**

```bash
gcloud config configurations list
```

### **Delete a configuration:**

```bash
gcloud config configurations delete config-name
```

---

### **Related Links**

- **[gcloud_projects.md]**: Learn how to manage projects and accounts in GCP.
- **[gcloud_billing.md]**: Configure and manage billing accounts associated with your projects.
- **[gcloud_iam_roles.md]**: Information about roles and permissions in GCP.

---

### **Notes**

- **Required Permissions:** Ensure you have the appropriate permissions to run authentication and configuration commands, such as `roles/iam.serviceAccountUser` or `roles/owner`.
- **Billing Accounts:** Authentication credentials are required to work with paid resources associated with billing accounts.
- **Access Tokens:** Tokens manually generated with `gcloud auth print-access-token` have a limited duration (usually 1 hour) and should not be used in production.
