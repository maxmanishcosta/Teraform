## TERRAFORM WORKSPACE:

In Terraform, a workspace is an isolated environment where a separate state file is maintained.

This feature allows you to manage different environments (like development, staging, production) within the same Terraform configuration.

Each workspace has its own state, enabling you to deploy the same infrastructure to multiple environments without needing to duplicate the configuration files.

**Key Concepts of Terraform Workspaces:**

**Isolation:** Each workspace has its own state file. This means the resources managed by Terraform in one workspace are isolated from those in another workspace.


## How Workspaces Work

When you initialize Terraform, you are in the default workspace. When you create a new workspace (e.g., prod), Terraform creates a separate state file for it.

**Local Backend:** Workspaces are stored in a directory called `terraform.tfstate.d/.`

**Remote Backend (S3/GCS):** Terraform adds a prefix to the state file path in your bucket to keep them separate.

`terraform workspace list` - Shows all existing workspaces.

`terraform workspace new dev` - Creates a new workspace named "dev".

`terraform workspace select prod` - Switches your current context to "prod".

`terraform workspace show` - Tells you which workspace you are currently using.

`terraform workspace delete dev` - Removes a workspace (must be empty/destroyed first).

The default workspace cannot be deleted

## The Terraform Configuration (`vi main.tf`)
```hcl
provider "aws" {
  region = "us-east-1"
}

locals {
  Define instance types based on the workspace name
  instance_types = {
    default = "t2.nano"
    dev     = "t2.micro"
    test    = "t2.small"
    prod    = "t3.medium"
  }
}

resource "aws_instance" "web_server" {
  Lookup the instance type based on the current workspace
  ami           = "ami-0c55b159cbfafe1f0" # Replace with a valid Amazon Linux 2 AMI
  instance_type = lookup(local.instance_types, terraform.workspace, "t2.micro")

  tags = {
    Name        = "WebServer-${terraform.workspace}"
    Environment = terraform.workspace
  }
}
```

**Step A: Initialize and Create Workspaces**

**Initialize the working directory
terraform init**

**Create the three workspaces**

`terraform workspace new dev`

`terraform workspace new test`

`terraform workspace new prod`

**Deploy to Dev**

`terraform workspace select dev`

`terraform plan`    - Verify Name is WebServer-dev and type is t2.micro

`terraform apply -auto-approve`

**Deploy to Test**

`terraform workspace select test`

`terraform apply -auto-approve` - Will create a separate WebServer-test (t2.small)

**Deploy to Prod**

`terraform workspace select prod`
`terraform apply -auto-approve` - Will create a separate WebServer-prod (t3.medium)

List all workspaces: `terraform workspace list`

**Check the State:** Terraform creates a folder named `terraform.tfstate.d/`. Inside, you will see subfolders for dev, test, and prod, each containing its own independent state file.

**Switching Environments:** To move between them, always use `terraform workspace select <name>`
