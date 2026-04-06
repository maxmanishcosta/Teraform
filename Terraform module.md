
## TERRAFORM MODULES


Terraform modules are a fundamental feature that helps in organizing and reusing Terraform configurations.

A module is a container for multiple resources that are used together.

Modules allow you to encapsulate and manage resources as a single unit, making your Terraform configurations more modular, readable, and maintainable.

**Root Module:**

The root module is the main configuration where Terraform starts its execution.

It is usually defined in the main configuration directory where terraform init and terraform apply are run.

The root module can call other modules, referred to as child modules.

**Child Modules:**

They help in organizing resources and reusing configurations.

Child modules are modules that are called from within other modules (including the root module).

Each child module can be stored in a separate directory and can be called using a module block in the root module or another parent module.
