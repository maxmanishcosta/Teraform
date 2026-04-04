## Version Constraints

Terraform version constraints allow you to specify which versions of Terraform or provider plugins your configuration is compatible with. 
This ensures that your infrastructure code is used with the correct version of Terraform or providers, avoiding unexpected behavior due to version mismatches.
We can change the versions of hashicorp provider plugins

**For Example:**

Whenever we have new changes on the AWS console, the old code might not work, so if you want to work with the new console or new features in AWS, we need to download the new provider plugins
https://registry.terraform.io/browse/providers

Select AWS and show versions
when we do terraform init, It will download always latest, if you are using old version just use below code to update version
All version plugins will be under .terraform --> go inside
Depending upon the version, the code will also change.
