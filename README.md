# Terraform Resource Module

Reusable Terraform modules for provisioning and managing Microsoft Azure infrastructure. This repository follows a modular, Git-based architecture that enables infrastructure code reuse across multiple projects.

## Overview

The goal of this repository is to build reusable Terraform modules for Azure resources. Each module is designed to be configurable and independently reusable across different infrastructure projects.

The modules support:

- Reusable Infrastructure as Code (IaC)
- Modular and maintainable Terraform configurations
- Git-based module integration
- Configurable resource deployment
- Integration with existing Azure resources using data sources
- Consistent infrastructure provisioning across projects

## Repository Structure

```text
Terraform-Resource-Module/
│
├── README.md
├── .gitignore
│
├── resource-group/
│   ├── main.tf
│   ├── variables.tf
│   ├── outputs.tf  (Optional)
│   └── data.tf     (Optional)
│
├── virtual-network/
│   ├── main.tf
│   ├── variables.tf
│   ├── outputs.tf  (Optional)
│   └── data.tf     (Optional)
│
├── subnet/
│   ├── main.tf
│   ├── variables.tf
│   ├── outputs.tf  (Optional)
│   └── data.tf     (Optional)
│
├── network-security-group/
│   ├── main.tf
│   ├── variables.tf
│   ├── outputs.tf  (Optional)
│   └── data.tf     (Optional)
│
├── public-ip/
│   ├── main.tf
│   ├── variables.tf
│   ├── outputs.tf  (Optional)
│   └── data.tf     (Optional)
│
├── nat-gateway/
│   ├── main.tf
│   ├── variables.tf
│   ├── outputs.tf  (Optional)
│   └── data.tf     (Optional)
│
├── bastion/
│   ├── main.tf
│   ├── variables.tf
│   ├── outputs.tf  (Optional)
│   └── data.tf     (Optional)
│
└── linux-vm/
    ├── main.tf
    ├── variables.tf
    ├── outputs.tf  (Optional)
    └── data.tf     (Optional)
```

**Note:** The directory structure represents the intended module organization. Each module can contain additional `.tf` files when required.

## Available Modules

| Module | Description |
|---|---|
| Resource Group | Creates Azure Resource Groups |
| Virtual Network | Creates Azure Virtual Networks |
| Subnet | Creates subnets within virtual networks |
| Network Security Group | Manages network security rules |
| Public IP | Creates Azure Public IP addresses |
| NAT Gateway | Configures outbound connectivity |
| Azure Bastion | Enables secure access to Azure virtual machines |
| Linux VM | Provisions Azure Linux Virtual Machines |

*Modules can be added or updated as the repository evolves.*

## Module File Structure

Each module uses Terraform configuration files according to its requirements.

| File | Purpose | Required |
|---|---|---|
| `main.tf` | Defines resources and core Terraform configuration | Recommended |
| `variables.tf` | Defines configurable input variables | Optional |
| `outputs.tf` | Exposes resource attributes to calling modules | Optional |
| `data.tf` | Defines data sources for reading existing resources | Optional |

### File Usage

**`main.tf`**

Contains Terraform resource blocks and other core configuration.

**`variables.tf`**

Defines input variables that allow users to customize resource names, locations, network ranges, and other configuration values.

**`outputs.tf`**

Defines outputs when a module needs to expose resource attributes to its parent module or consuming project.

**`data.tf`**

Contains data source blocks used to retrieve information about existing Azure resources.

These files are organizational conventions. Terraform loads all `.tf` files in the same module directory, so data sources and outputs can also be defined in other `.tf` files.

## Technologies Used

- Terraform
- Microsoft Azure
- AzureRM Terraform Provider
- Azure CLI
- HCL
- Git and GitHub

## Prerequisites

Before using these modules, ensure you have:

- An active Azure subscription
- Terraform installed
- Azure CLI installed
- Git installed
- Appropriate permissions to access or provision the required Azure resources

## Azure Authentication

Sign in to Azure using Azure CLI:

```bash
az login
```

Check the active Azure subscription:

```bash
az account show
```

Select a subscription if necessary:

```bash
az account set --subscription "<SUBSCRIPTION_ID>"
```

Use an appropriate authentication method for your local environment or CI/CD pipeline.

## Usage

Modules can be called from another Terraform configuration using their Git repository URL.

### Example: Calling the Resource Group Module

```hcl
module "resource_group" {
  source = "git::https://github.com/Abhishek3758sharma/Terraform-Resource-Module.git//resource-group?ref=v1.0.0"

  name     = "rg-demo-project"
  location = "Central India"
}
```

The variable names in this example are illustrative. They must match the actual input variables defined in the `resource-group` module.

The `v1.0.0` reference must correspond to a Git tag that exists in the repository.

### Initialize Terraform

```bash
terraform init
```

### Format Terraform Files

```bash
terraform fmt -recursive
```

### Validate Configuration

```bash
terraform validate
```

### Review Infrastructure Changes

```bash
terraform plan
```

### Deploy Infrastructure

```bash
terraform apply
```

Review the execution plan and confirm the proposed changes before deployment.

## Using Data Sources

Data sources allow Terraform to retrieve information about existing Azure resources instead of creating those resources again.

For example, to reference an existing Azure Resource Group:

```hcl
data "azurerm_resource_group" "existing" {
  name = "rg-existing-project"
}
```

The resource group location can then be referenced as:

```hcl
location = data.azurerm_resource_group.existing.location
```

The example assumes the AzureRM provider is configured and the resource group exists and is accessible.

## Git-Based Module Versioning

Modules can be referenced using Git tags to maintain consistent versions across projects.

Create and push a version tag:

```bash
git tag v1.0.0
git push origin v1.0.0
```

Reference the tagged version in a Terraform configuration:

```hcl
module "resource_group" {
  source = "git::https://github.com/Abhishek3758sharma/Terraform-Resource-Module.git//resource-group?ref=v1.0.0"

  # Configure arguments according to the module's variables.
}
```

Use version tags to control which module revision a project consumes.

## Best Practices

- Keep modules focused on specific Azure resources or related functionality.
- Use input variables instead of hardcoding environment-specific values.
- Define outputs only when they are needed.
- Use data sources to reference existing resources when appropriate.
- Validate resource names, locations, and other inputs.
- Pin module references to stable Git tags.
- Follow consistent naming conventions.
- Avoid duplicating Terraform code across projects.
- Never commit credentials, passwords, access tokens, or secret values.
- Review Terraform plans before applying changes.
- Use least-privilege permissions for Azure access.

## Roadmap

- [ ] Implement the Resource Group module
- [ ] Implement the Virtual Network module
- [ ] Implement the Subnet module
- [ ] Implement the Network Security Group module
- [ ] Implement the Public IP module
- [ ] Implement the NAT Gateway module
- [ ] Implement the Azure Bastion module
- [ ] Implement the Linux VM module
- [ ] Add module-specific usage examples
- [ ] Add input validation and documentation
- [ ] Introduce versioned releases
- [ ] Integrate Terraform validation and security scanning into CI/CD

## Contributing

Contributions and improvements are welcome.

1. Create a feature branch.
2. Implement the required changes.
3. Run `terraform fmt -recursive`.
4. Validate the relevant Terraform configurations.
5. Submit a pull request with a clear description of the changes.

## Author

**Abhishek Sharma**

- 🌐 **Portfolio:** [abhivox.online](https://abhivox.online)
- 💻 **GitHub:** [Abhishek3758sharma](https://github.com/Abhishek3758sharma)

---

⭐ If you find these Terraform modules useful, consider starring this repository!
