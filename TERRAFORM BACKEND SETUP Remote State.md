## TERRAFORM BACKEND SETUP

**Remote State:**

"By default, Terraform stores state locally in a file named terraform.tfstate. When working with Terraform in a team, use of a local file makes Terraform usage complicated because each user must make sure they always have the latest state data before running Terraform and make sure that nobody else runs Terraform at the same time."
"With remote state, Terraform writes the state data to a remote data store (S3), which can then be shared between all members of a team."

Generally, we have the statefile in local, if you lost the machine, the statefile is also lost. So that reason we keep statefile in S3
And also, all DevOps Engineers can share the statefile if required.

**First, create an S3 Private bucket with Versioning**

```hcl
vi main.tf
provider "aws" {
  region = "ap-south-1"
}
terraform {
  backend "s3" {
    bucket = "terraform-statefile-reyaz"
    key    = "prod/terraform.tfstate"
    region = "ap-south-1"
  }
}
resource "aws_instance" "myfirstinstance" {
  ami           = "ami-0492447090ced6eb5"
  instance_type = "t2.micro"
  tags = {
    Name = "backend-example1"
  }
}
resource "aws_instance" "mysecondinstance" {
  ami           = "ami-0492447090ced6eb5"
  instance_type = "t2.micro"
  tags = {
    Name = "backend-example2"
  }
}
```

-- `terraform init`

-- `terraform apply --auto-approve `

**Note: Now see the terraform.tfstate in the S3 bucket**

General Note: If you modify myfirstinstance or mysecondinstance, it will destroy the existing server and create a new one, but if you want to modify the tag, 
Just change the tag to something else and terraform apply, the server will not be destroyed, only the tag will change.

-- `terraform state list`

-- `terraform destroy --auto-approve -target="aws_instance.myfirstinstance"` [This will destroy only one instance and update in S3 statefile]

-- `cat terraform.tfstate` [Currently no resources are there]

-- `cat terraform.tfstate.backup` [This is the backup of the previous state]


