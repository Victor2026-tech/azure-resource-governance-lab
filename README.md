# Azure Resource Governance Strategy

## Azure Resource Hierarchy

Microsoft Azure organizes resources in a hierarchical structure to simplify management, governance, and access control.

```text
Azure Tenant
│
└── Azure Subscription (Free Trial)
    │
    ├── Resource Group: rg-webapp-dev-eastus
    │     └── Storage Account: stwebappdeveastus
    │
    ├── Resource Group: rg-webapp-prod-eastus
    │     └── Storage Account: stwebappprodeastus
    │
    └── Resource Group: rg-temp-dev-eastus
          └── Storage Account: sttempdeveastus
```

### Hierarchy Explanation

* **Tenant** – The highest level of Azure identity management that contains users, groups, and subscriptions.
* **Subscription** – A billing and management boundary used to organize Azure resources.
* **Resource Group** – A logical container that groups resources sharing the same lifecycle or purpose.
* **Resources** – Individual Azure services such as Storage Accounts, Virtual Machines, and SQL Databases.

---

# Resource Group Strategy

The project separates resources according to environment.

| Resource Group        | Purpose                                                                    |
| --------------------- | -------------------------------------------------------------------------- |
| rg-webapp-dev-eastus  | Development environment used for testing and experimentation.              |
| rg-webapp-prod-eastus | Production environment used for live workloads.                            |
| rg-temp-dev-eastus    | Temporary environment used to test lifecycle management and bulk deletion. |

### Why this strategy?

Separating environments provides several advantages:

* Prevents development activities from affecting production systems.
* Makes it easier to assign different permissions to development and production teams.
* Simplifies resource cleanup by deleting an entire Resource Group when it is no longer needed.
* Supports future scalability by allowing additional environments (Test, QA, Staging) to be created using the same naming standard.

---

# Tagging Strategy

The following tags were applied to Azure Resource Groups and resources.

| Tag         | Example Value            | Purpose                                          |
| ----------- | ------------------------ | ------------------------------------------------ |
| environment | development / production | Identifies deployment environment.               |
| owner       | TeamA / TeamB            | Identifies the responsible team.                 |
| project     | AzureLab                 | Groups all resources belonging to this project.  |
| lifecycle   | temporary                | Identifies resources that can safely be deleted. |
| costCenter  | IT001                    | Supports cost allocation and budgeting.          |

### Benefits of Tagging

* Improves cost tracking.
* Enables automation through Azure scripts and policies.
* Simplifies resource searching and filtering.
* Helps identify ownership of resources.

---

# Governance Strategy

## Role-Based Access Control (RBAC)

The following RBAC model was designed for this project.

| Team            | Resource Group        | Role        |
| --------------- | --------------------- | ----------- |
| TeamA           | rg-webapp-prod-eastus | Contributor |
| TeamB           | rg-webapp-dev-eastus  | Contributor |
| Operations Team | All Resource Groups   | Reader      |

### RBAC Rationale

* TeamA manages production resources.
* TeamB develops and tests applications in the development environment.
* Operations personnel require read-only access for monitoring and auditing.

Because this project was completed using a single Azure Free Trial account, the RBAC assignments were documented as a simulated enterprise environment.

---

# Azure Policy

In a production environment, Azure Policy would be used to:

* Enforce approved naming conventions.
* Require mandatory tags such as Environment and Owner.
* Prevent deployment into unauthorized regions.
* Restrict the creation of unsupported resource types.

---

# Lifecycle Management

The Resource Group **rg-temp-dev-eastus** was created specifically to test Azure lifecycle management.

A Storage Account was deployed into the Resource Group and later deleted by deleting the Resource Group itself.

This demonstrates Azure's ability to perform bulk deletion, where all resources within a Resource Group are automatically removed.

---

# Conclusion

This project demonstrates Azure governance principles through consistent naming conventions, environment-based resource organization, tagging, RBAC planning, lifecycle management, and governance best practices.

