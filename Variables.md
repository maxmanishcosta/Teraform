## VARIABLES

In Terraform, variables are used to make configurations more dynamic and reusable.
Terraform variables are a core feature that allows you to parameterize your Terraform configurations.
It's a block in terraform used to define the variables.
By using variables, you can make your code more flexible, reusable, and easier to manage.
Variables enable you to customize your Terraform deployments without hardcoding values directly into your configuration files.

**Types of Terraform Variables**

**Input Variables:** These allow you to pass values into Terraform configurations. They are defined using the variable block.

**Output Variables:** These are used to return values from your Terraform configurations after they have been applied, sharing data between different configurations or modules.

**Local Variables:** These are used to assign values to an expression or value within a configuration for reuse, improving readability and maintainability.

## Variable Types

**Terraform supports several types of variables:**

**string:** A sequence of characters ("hello", "world")

**number:** Any numeric value (10, 3.14, -5)

**bool:** A boolean value (true or false)

**list(type):** An ordered list of elements ("a, "b", "c")

**map(type):** A key-value pair mapping ({key1 = "value1", key2 = "value2" })

**set(type):** A unique unordered collection of elements ("a", "b", "c")

**object({...}):** A structured object with named attributes

**tuple([types]):** A fixed sequence of elements with different types

