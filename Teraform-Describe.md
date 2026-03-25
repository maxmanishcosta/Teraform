## Terraform command

- terraform init - The terraform init command initializes a working directory containing Terraform configuration files.
- terraform plan - Creates an execution plan (dry run)
- terraform apply - Executes changes to the actual environment
- terraform apply -auto-approve - Apply changes without being prompted to enter "yes."
- terraform destroy -auto-approve - Destroy/cleanup without being prompted to enter "yes"


All tf code should be written in .tf files, extension is .tf, also called configuration files

## Main things in TF file

- Blocks
- Labels
- argument

A tf file has blocks, for example, provider is a block, "aws" is a label, for a single block we can have multiple labels 0, 1, or 2, etc., optional

Whatever we write in {} is called arguments, arguments can be called as input for the block, arguments need to have a key and a value

For the provider, we have one label AWS, but for the resource block, it has 2 labels, which can be multiple labels _
is called an identifier. If you want to combine 2 words, use _

We cannot use AWS instance (space between), so use aws_instance, instance_type.








