## Provisioners

Provisioners are used to execute scripts or shell commands on a local machine or a remote resource as part of the resource creation or destruction process.

While they sound useful, they are considered a "last resort." Terraform is a declarative tool (focused on the "what"), whereas provisioners are imperative (focused on the "how").

**Types of Provisioners**

**local-exec:** Runs a command on the machine executing Terraform (e.g., your laptop or a CI/CD runner).

   Use case: Saving an IP address to a local file or triggering a local configuration script.

   **remote-exec:** Invokes a script on a remote resource after it is created. This requires a connection block (SSH or WinRM).

Use case: Installing a specific software package or starting a service immediately after a VM boots.


**Example**

```
resource "aws_instance" "web" {
  ami           = "ami-12345678"
  instance_type = "t2.micro"

  # local-exec: Runs on your computer
  provisioner "local-exec" {
    command = "echo ${self.private_ip} >> private_ips.txt"
  }

  # remote-exec: Runs on the AWS instance
  provisioner "remote-exec" {
    inline = [
      "sudo apt-get update",
      "sudo apt-get install -y nginx",
    ]

    connection {
      type     = "ssh"
      user     = "ubuntu"
      password = var.root_password
      host     = self.public_ip
    }
  }
}
```
