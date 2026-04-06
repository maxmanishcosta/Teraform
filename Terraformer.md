## Terraformer

Terraformer is a CLI tool written in Go that performs Reverse Terraform. It infrastructure-scans your existing cloud resources and generates the corresponding `.tf files` and `terraform.tfstate`.

If we want to import bulk, then we can use the Terraformer tool. 

**Install terraformer**

vi terraformer.sh
```
sudo yum update -y
sudo yum install -y wget unzip
wget https://github.com/GoogleCloudPlatform/terraformer/releases/download/0.8.24/terraformer-aws-linux-amd64 -O terraformer
chmod +x terraformer
sudo mv terraformer /usr/local/bin/
echo 'export PATH=$PATH:/usr/local/bin' >> ~/.bashrc
source ~/.bashrc
terraformer --version
```
`source ~/.bashrc`

launch 3 ec2 instances manually

`terraformer import aws --resources=ec2_instance --regions=ap-south-1`

Can import the entire VPC, subnet also.

`terraformer import aws --resources=instance,vpc,subnet --regions=ap-south-1`

