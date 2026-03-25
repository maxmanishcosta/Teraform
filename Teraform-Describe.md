## Terraform command

- `terraform fmt` [used to format your configuration files into a canonical format and style]
- `terraform fmt -recursive` --for all files
- `terraform init` - The terraform init command initializes a working directory containing Terraform configuration files.
- `terraform plan` - Creates an execution plan (dry run)
- `terraform apply` - Executes changes to the actual environment
- `terraform apply -auto-approve` - Apply changes without being prompted to enter "yes."
- `terraform destroy -auto-approve` - Destroy/cleanup without being prompted to enter "yes"


All tf code should be written in .tf files, extension is .tf, also called configuration files

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

vi main.tf

provider "aws" {
region "ap-south-1"
}

-------------------------

- provider is block
- AWS is a label
- {} inside are arguments

----------------------------

## terraform init
Whenever you have a new or existing Terraform directory (containing your Terraform configuration files), you need to run terraform init to prepare that directory for other Terraform commands.


**Provider Plugins:** Terraform uses plugins to interface with cloud providers (like AWS, Azure, Google Cloud, etc.). The init command checks the configuration files to see which providers you're using and fetches the required provider plugins.

**Provider Versions:** If you've specified a particular version of a provider in your configuration, terraform init will download that version. If not, it'll get the latest compatible version.



