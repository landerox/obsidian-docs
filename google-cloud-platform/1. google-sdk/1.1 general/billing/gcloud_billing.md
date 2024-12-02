
Labels: #gcp #billing
Description: Configuration and management of billing accounts (`gcloud billing accounts list`, `gcloud billing projects link`).
Related to: [[gcloud_projects.md]], [[gcloud_auth.md]]

##### **List available billing accounts**

```bash
gcloud billing accounts list
```

This command lists the available billing accounts associated with your user or organization.

##### **Get information about a specific billing account**

```bash
gcloud billing accounts describe [ACCOUNT_ID]
```

Replace `[ACCOUNT_ID]` with the account identifier.

##### **Check if a project has billing enabled**

```bash
gcloud beta billing projects describe [PROJECT_ID]
```

Replace `[PROJECT_ID]` with the project ID.

##### **Link a project to a billing account**

This command enables billing for a project by linking it to a billing account.

```bash
gcloud beta billing projects link [PROJECT_ID] --billing-account [ACCOUNT_ID]
```

##### **Disable billing for a project**

This command disables billing for the project.

```bash
gcloud beta billing projects unlink [PROJECT_ID]
```

**Note:** Disabling billing does not delete existing resources, but it may suspend services that depend on it.

##### **Create a budget alert with a defined limit:**

```bash
gcloud billing budgets create     --billing-account [ACCOUNT_ID]     --display-name "My Budget"     --amount 100.00     --threshold-rules "0.5=EMAIL,1.0=EMAIL"
```

- **`--amount`**: Sets the budget limit (in dollars).
- **`--threshold-rules`**: Defines thresholds for alerts; in this case, 50% and 100%.

##### **List existing budgets:**

```bash
gcloud billing budgets list --billing-account [ACCOUNT_ID]
```

##### **Delete a budget:**

```bash
gcloud billing budgets delete [BUDGET_NAME]
```

##### **Related Links**

- [[gcloud_auth.md]]: Learn how to authenticate to manage billing accounts.
- [[gcloud_projects.md]]: How to create and manage projects before linking them to billing accounts.
- [[gcloud_monitoring_alerts.md]]: How to set up monitoring policies and cost-related alerts.

##### **Notes**

- **Required permissions**: To manage billing accounts, you need the `roles/billing.admin` role or specific permissions in the organization. To link projects to billing accounts, you need to be the owner or editor of the project.
- **Billing accounts**: Set up billing accounts before linking them to projects to enable paid resources.
- **Billing limits**: Configure budgets and cost alerts to avoid unexpected charges using the budget commands.
- **Official documentation**: Check the official Google Cloud billing documentation for more details and advanced use cases.
