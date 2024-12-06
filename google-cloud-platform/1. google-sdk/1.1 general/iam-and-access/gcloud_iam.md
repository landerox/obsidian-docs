
**Tags:** #gcp #iam #roles
**Description:** Commands to manage roles, permissions, and access policies (`gcloud iam roles`, `gcloud iam policy`).
**Related to:** [[gcloud_projects.md]], [[gcloud_auth.md]]

### **List available roles**

```bash
gcloud iam roles list
```

Displays all the roles available in your project or organization.

### **Create a custom role**

```bash
gcloud iam roles create [ROLE_ID] \
    --project=[PROJECT_ID] \
    --title="Custom Role" \
    --description="Description of custom role" \
    --permissions="permission1,permission2" \
    --stage="GA"
```

- **[ROLE_ID]**: Unique identifier for the role.
- **[PROJECT_ID]**: Project where the role will be created.

### **Update an existing role**

```bash
gcloud iam roles update [ROLE_ID] --project=[PROJECT_ID] --permissions="permission1,permission3"
```

### **Delete a custom role**

```bash
gcloud iam roles delete [ROLE_ID] --project=[PROJECT_ID]
```

### **Assign a role to a user**

```bash
gcloud projects add-iam-policy-binding [PROJECT_ID] \
    --member="user:email@example.com" \
    --role="roles/[ROLE_NAME]"
```

### **Revoke a role from a user**

```bash
gcloud projects remove-iam-policy-binding [PROJECT_ID] \
    --member="user:email@example.com" \
    --role="roles/[ROLE_NAME]"
```

### **View IAM policies**

```bash
gcloud projects get-iam-policy [PROJECT_ID]
```

---

### **Related Links**

- **[gcloud_auth.md]**: Learn how to authenticate for accessing and managing IAM policies.
- **[gcloud_projects.md]**: How to manage projects, essential for assigning roles and permissions.
- **[gcloud_iam_roles.md]**: More detailed information about default and custom roles in GCP.
- **[gcloud_iam_policies.md]**: Advanced management of access policies and audits.
- **[gcloud_monitoring_alerts.md]**: Configure alerts to monitor changes in roles or policies.

---

### **Notes**

- **Required Permissions**: Requires `roles/owner` or `roles/iam.admin` to execute advanced IAM commands.
- **Organizational Policies**: Configure policies at higher levels, such as organizations or folders, if necessary.
- **Official Documentation**: Refer to the official documentation for specific roles and advanced use cases.
