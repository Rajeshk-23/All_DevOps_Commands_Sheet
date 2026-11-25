# Terraform Cheatsheet

> Terraform is an infrastructure-as-code tool for safely provisioning and managing cloud and service resources.

## Table of Contents
- [Init & Setup](#init--setup)
- [Plan & Apply](#plan--apply)
- [State Management](#state-management)
- [Workspaces](#workspaces)
- [Formatting & Validation](#formatting--validation)
- [Modules](#modules)
- [Import](#import)
- [Output](#output)
- [Destroy](#destroy)
- [Providers](#providers)
- [Debugging](#debugging)

## Init & Setup

| Command | Description |
| --- | --- |
| `terraform init` | Initialize a working directory and download required providers. |
| `terraform init -upgrade` | Initialize and upgrade providers and modules within version constraints. |
| `terraform init -reconfigure` | Reconfigure the backend without migrating existing state. |
| `terraform init -migrate-state` | Initialize and migrate state to the configured backend. |
| `terraform init -backend=false` | Initialize providers and modules without configuring a backend. |
| `terraform version` | Display the Terraform version and installed provider versions. |

## Plan & Apply

| Command | Description |
| --- | --- |
| `terraform plan` | Preview infrastructure changes without applying them. |
| `terraform plan -out=tfplan` | Save an execution plan to a file for later application. |
| `terraform plan -var-file=prod.tfvars` | Plan using variable values from a specified file. |
| `terraform plan -target=aws_instance.web` | Plan changes for a specific resource and its dependencies. |
| `terraform apply` | Apply the proposed infrastructure changes interactively. |
| `terraform apply tfplan` | Apply a previously saved execution plan. |
| `terraform apply -auto-approve` | Apply changes without requesting interactive approval. |

## State Management

| Command | Description |
| --- | --- |
| `terraform state list` | List all resource addresses tracked in the current state. |
| `terraform state show aws_instance.web` | Show the state attributes for one resource. |
| `terraform state pull` | Download and print the current remote state as JSON. |
| `terraform state push terraform.tfstate` | Upload a local state file to the configured backend. |
| `terraform state mv aws_instance.old aws_instance.new` | Move a resource to a new address in state. |
| `terraform state rm aws_instance.legacy` | Remove a resource from state without destroying it remotely. |
| `terraform state replace-provider hashicorp/aws registry.terraform.io/hashicorp/aws` | Replace provider references in state. |
| `terraform state list 'module.network.*'` | List only resources matching an address pattern. |
| `terraform refresh` | Reconcile state with real infrastructure without changing resources. |
| `terraform apply -refresh-only` | Refresh state through the normal plan and apply workflow. |

## Workspaces

| Command | Description |
| --- | --- |
| `terraform workspace list` | List available workspaces and mark the current one. |
| `terraform workspace show` | Print the name of the current workspace. |
| `terraform workspace new staging` | Create and switch to a new workspace. |
| `terraform workspace select production` | Switch to an existing workspace. |
| `terraform workspace delete staging` | Delete an empty non-current workspace. |
| `terraform workspace select default` | Switch back to the default workspace. |

## Formatting & Validation

| Command | Description |
| --- | --- |
| `terraform fmt` | Format Terraform configuration files in the current directory. |
| `terraform fmt -recursive` | Format Terraform files in the current directory and subdirectories. |
| `terraform fmt -check` | Check formatting without modifying files. |
| `terraform validate` | Validate configuration syntax and internal consistency. |
| `terraform validate -json` | Emit validation results in machine-readable JSON. |

## Modules

| Command | Description |
| --- | --- |
| `terraform get` | Download and update modules required by the configuration. |
| `terraform get -update` | Update already-downloaded modules to allowed newer versions. |
| `terraform providers` | Show provider requirements for the configuration and state. |
| `terraform providers lock -platform=linux_amd64` | Add provider checksums for a target platform to the lock file. |
| `terraform providers mirror ./provider-mirror` | Mirror required provider packages into a local directory. |

## Import

| Command | Description |
| --- | --- |
| `terraform import aws_instance.web i-0123456789abcdef0` | Import an existing resource into a configured resource address. |
| `terraform import -var-file=prod.tfvars aws_s3_bucket.logs my-logs-bucket` | Import using variable values from a file. |
| `terraform import -config=./infra aws_vpc.main vpc-0123456789abcdef0` | Import using configuration from another directory. |
| `terraform plan -generate-config-out=generated.tf` | Generate configuration for import blocks when planning imports. |

## Output

| Command | Description |
| --- | --- |
| `terraform output` | List all output values from the current state. |
| `terraform output public_ip` | Print one named output value. |
| `terraform output -json` | Emit all output values as JSON. |

## Destroy

| Command | Description |
| --- | --- |
| `terraform destroy` | Destroy all resources managed by the current configuration. |
| `terraform destroy -target=aws_instance.web` | Destroy a specific resource and its dependent resources. |

## Providers

| Command | Description |
| --- | --- |
| `terraform providers schema -json` | Export installed provider schemas as JSON. |
| `terraform providers lock -platform=darwin_arm64` | Record provider checksums for macOS on Apple Silicon. |
| `terraform init -plugin-dir=./plugins` | Initialize using provider plugins from a local directory. |
| `terraform init -lockfile=readonly` | Verify the dependency lock file without modifying it. |

## Debugging

| Command | Description |
| --- | --- |
| `terraform console` | Open an interactive console for evaluating Terraform expressions. |
| `terraform graph` | Generate a dependency graph in DOT format. |
| `terraform graph | dot -Tsvg > graph.svg` | Render the dependency graph as an SVG file. |
| `TF_LOG=DEBUG terraform plan` | Run a plan with detailed Terraform debug logging. |
| `TF_LOG=TRACE TF_LOG_PATH=terraform.log terraform apply` | Write trace-level Terraform logs to a file during apply. |
