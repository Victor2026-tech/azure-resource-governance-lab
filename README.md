# Azure Resource Governance Lab

## Naming Convention

### Subscription Naming Convention

Format:

sub-<environment>-<organization>

Examples:

* sub-dev-vcm
* sub-prod-vcm

Note: The Azure Free Trial subscription provided by Microsoft was used for implementation. The naming convention above represents the organization's proposed standard for future subscriptions.

### Resource Group Naming Convention

Format:

rg-<application>-<environment>-<region>

Examples:

* rg-webapp-dev-eastus
* rg-webapp-prod-eastus
* rg-temp-dev-eastus

### Virtual Machine Naming Convention

Format:

vm-<application>-<environment>-<number>

Example:

* vm-webapp-dev-01

### Storage Account Naming Convention

Format:

st<application><environment><region>

Example:

* stwebappdeveastus
