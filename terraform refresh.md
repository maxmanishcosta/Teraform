## terraform refresh

In Terraform, terraform refresh is a command used to reconcile the state file with the real-world infrastructure. It queries your cloud provider (AWS, Azure, etc.) to see if any settings have changed 
outside of Terraform and updates the `.tfstate` file to reflect the current truth.

**What does it actually do?**

Imagine you deployed an EC2 instance using Terraform. Later, someone manually changed the Instance Type in the AWS Console from t2.micro to `t2.small`.

Your Code says: `t2.micro`

Your State File says: `t2.micro`

The Real World is: `2.small`

Running terraform refresh will update the State File to `t2.small`. It does not modify your code and it does not change your cloud resources; it only updates the "map" (the state).

**Risks of Refresh**

Sensitive Data: If a manual change added sensitive information to a resource, refresh will pull that data into your state file in plain text.

State Locking: On large projects, a refresh can take a long time and will lock the state, preventing others from running plans or applies.

Accidental Alignment: If you accidentally refresh against the wrong environment, you might update your state with data from a different account.

