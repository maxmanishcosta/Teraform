# Install Terraform

## Windows

1. Install Terraform from the Downloads [Page](https://developer.hashicorp.com/terraform/downloads)

(or)

2. Use GitHub Codespaces (Free for 60 hours per month)

- Login to your GitHub account
- Click on the Profile Icon to the top right
- Click on "your codespaces" as shown in the [Image](../Images/codespaces-location.png)
- Codespaces will provide you a virtual machine with Ubuntu and VS Code by default.
- Follow the steps provided in the Downloads [Page](https://developer.hashicorp.com/terraform/downloads) for Linux.

## Linux

- Follow the steps provided in the Downloads [Page](https://developer.hashicorp.com/terraform/downloads) for Linux.

## macOS

- Follow the steps provided in the Downloads [Page](https://developer.hashicorp.com/terraform/downloads) for macOS.

## Installing Terraform on Amazon Linux 2

- Launch an Amazon Linux 2 instance and attach a role with admin permissions.

- sudo yum update -y
- sudo yum install -y yum-utils
- sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/AmazonLinux/hashicorp.repo
- sudo yum install -y terraform
- terraform version

## Installing Terraform on Ubuntu

- apt update -y
- apt install awscli -y
- wget -O - https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
- echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
- sudo apt update && sudo apt install terraform

- terraform -v





