
**Tags:** #gcp #projects
**Description:** Project and account management in GCP (`gcloud projects list`, `gcloud organizations`).
**Related to:** [[gcloud_auth.md]], [[gcloud_billing.md]]

### **List Projects**

Command to view all available projects associated with your active account:

```bash
gcloud projects list
```

This command displays a table with:

- **Project ID**: Unique identifier for the project.
- **Name**: Name of the project.
- **Project Number**: Unique number assigned by GCP.
- **Lifecycle State**: Current state of the project (e.g., ACTIVE).

### **Create a New Project**

You can create a project using the following command:

```bash
gcloud projects create [PROJECT_ID] --name="[PROJECT_NAME]"
```

- **[PROJECT_ID]**: A unique identifier for the project (lowercase letters, numbers, and hyphens).
- **[PROJECT_NAME]**: Human-readable name for the project.

Associate the project with a specific billing account:

```bash
gcloud projects create [PROJECT_ID] --name="[PROJECT_NAME]" --billing-account="[BILLING_ACCOUNT_ID]"
```

### **Change the Active Project**

To work with a specific project, you need to set it as active:

```bash
gcloud config set project [PROJECT_ID]
```

You can check which project is currently active:

```bash
gcloud config get-value project
```

### **Delete a Project**

To delete a project (note that all data and resources will be lost):

```bash
gcloud projects delete [PROJECT_ID]
```

### **View Organizations**

To list all organizations associated with your account:

```bash
gcloud organizations list
```

### **Move a Project to an Organization**

If you need to assign a project to a specific organization:

```bash
gcloud projects move [PROJECT_ID] --organization=[ORG_ID]
```

---

### **Related Links**

- **[gcloud_auth.md]**: Learn how to authenticate and configure your GCP account before managing projects.
- **[gcloud_billing.md]**: Configuration and management of billing accounts associated with your projects.

---

### **Notes**

- **Required Permissions**: Ensure you have the appropriate permissions to manage projects, such as `roles/resourcemanager.projectCreator` or `roles/owner`.
- **Billing Accounts**: Every project must be associated with a billing account to enable paid resources.
