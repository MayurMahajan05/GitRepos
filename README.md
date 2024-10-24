

provider "aws" {

region = "us-west-2"

access_key = "my-access-key"

secret_key = "my-secret-key"

}

resource "aws_instance" "terraform_ec2_example" {

ami = "ami-0c1a7f89451184c8b" # us-west-2

instance_type = "t2.micro"

tags = {

Name = "Terraform ec2"

}

}
