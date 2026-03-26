## Terraform command

- `terraform fmt` [used to format your configuration files into a canonical format and style]
- `terraform fmt -recursive` --for all files
- `terraform init` - The terraform init command initializes a working directory containing Terraform configuration files.
- `terraform plan` - Creates an execution plan (dry run)
- `terraform apply` - Executes changes to the actual environment
- `terraform apply -auto-approve` - Apply changes without being prompted to enter "yes."
- `terraform destroy -auto-approve` - Destroy/cleanup without being prompted to enter "yes"


All tf code should be written in `.tf` files, extension is .tf, also called configuration files

## Main things in TF file

- Blocks
- Labels
- argument

A tf file has blocks, for example, provider is a block, "aws" is a label, for a single block we can have multiple labels 0, 1, or 2, etc., optional

Whatever we write in {} is called an argument. Arguments can be called as input for the block, arguments need to have a key and a value

For the provider, we have one label AWS, but for the resource block, it has 2 labels, which can be multiple labels _
is called an identifier. If you want to combine 2 words, use _

We cannot use AWS instance (space between), so use aws_instance, instance_type.

## First TF Example
```
vi main.tf

provider "aws" {
region "ap-south-1"
}
```
-------------------------

- provider is block
- AWS is a label
- {} inside are arguments

----------------------------

## terraform init
Whenever you have a new or existing Terraform directory (containing your Terraform configuration files), you need to run terraform init to prepare that directory for other Terraform commands.


**Provider Plugins:** Terraform uses plugins to interface with cloud providers (like AWS, Azure, Google Cloud, etc.). The init command checks the configuration files to see which providers you're using and fetches the required provider plugins.

**Provider Versions:** If you've specified a particular version of a provider in your configuration, terraform init will download that version. If not, it'll get the latest compatible version.

## STATE FILE

**What is a state, and why is it important in Terraform?**

"Terraform must store state about your managed infrastructure and configuration. This state is used by Terraform to map real world resources to your configuration, keep track of metadata, and to improve performance for large infrastructures. This state file is extremely important; it maps various resource metadata to actual resource IDs so that Terraform knows what it is managing. This file must be saved and distributed to anyone who might run Terraform."


**Local State and Remote State:**

"By default, Terraform stores state locally in a file named `terraform.tfstate`. When working with Terraform in a team, 
The use of a local file makes Terraform usage complicated because each user must make sure they always have the latest state data before running 
Terraform and make sure that nobody else runs Terraform at the same time."

"With remote state, Terraform writes the state data to a remote data store, which can then be shared between all members of a team." Ex: 53

- `cat terraform.tfstate`
- `terraform state list` - Terraform command used to list all the resources that are currently being tracked in the Terraform state file
- `terraform destroy --auto-approve`

## .terraform.lock.hcl

When you run `terraform init`, Terraform downloads the required providers and dependencies and generates the terraform.lock.hcl file if it doesn't already exist. If the file does exist, Terraform checks the versions specified in the lock file and installs those versions.

The `terraform.lock.hcl` file is a lock file used by Terraform to manage the dependencies of your Terraform project. It ensures that the same versions of provider plugins and modules are used every time you run Terraform, making your infrastructure deployments more predictable and consistent.

**Purpose:** Dependency Management, Consistency and Security

- `.terraform.lock.hcl`

## Current State vs Desired State

The current state represents the actual state of your infrastructure resources as they exist in the real world (e.g., in your cloud provider). Terraform tracks the current state of your infrastructure in a state file (`terraform.tfstate`).

The desired state is what you define in your Terraform configuration files. It represents the infrastructure that you want Terraform to create, update, or destroy. You define the desired state using HashiCorp Configuration Language (HCL) in `.tf` files

## Example: Launching 5 EC2 instances using the - COUNT Argument

vi main.tf
```
provider "aws" {
region "ap-south-1"
}
resource "aws_instance" "myinstance" {
count = 5
ami = "ami-0492447090ced6ebs"
instance_type = "t2.micro"
}
```
- `terraform apply --auto-approve`
- `terraform state list` - list all resources 

## TARGET

**It is used to delete a specific resource**
- `terraform state list` - list all resources 
- `terraform destroy --auto-approve -target=resources_name` - to delete a single resource
- `terraform destroy --auto-approve -target=resources_name -target=resources_name` - to delete multiple resources at same time
