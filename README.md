sudo systemctl start jenkins
sudo systemctl status jenkins

pipeline {
    agent any
    stages {
        stage('Code') {
            steps {
                echo 'This is a build phase'
            }
        }
        stage('Build') {
            steps {
                input('Do you want to continue?')
            }
        }
        stage('Integrate') {
            when {
                not {
                    branch 'master'
                }
            }
            steps {
                echo 'Integration is done!!!'
            }
        }
        stage('Test') {
            parallel {
                stage('Unit Test') {
                    steps {
                        echo 'Unit test done'
                    }
                }
                stage('Integration Test') {
                    steps {
                        echo 'Running Integration Test'
                    }
                }
            }
        }
    }
}


FROM nginx
COPY index.html/usr/share/nginx/html 


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
