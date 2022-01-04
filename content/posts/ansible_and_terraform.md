---
title: "Intro to terraform"
date: 2021-12-12T18:20:56+02:00
draft: true
---

terraform is cloud provider agnostic infrastructure as code tool from hashicorp, it provides a cli to manage cloud services, 

infrastructure is defined in a text format language known as HCL

terraform uses plugins which they call providers to interface with cloud provides such as aws, azure, etc

### example terraform and aws
 ```
 # main.tf
 
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 3.27"
    }
  }
  required_version = ">=0.14.9"

}

provider "aws" {

  profile = "default"
  region  = "af-south-1" #replace with your region
}

resource "aws_instance" "app_server" {

  ami           = "ami-08a4b40f2fe1e4b35" #replace with an ami in your region
  instance_type = "t3.micro"

  tags = {
    Name = var.instance_name
  }
}


 ```
 
 ```
#variables.tf 
variable "instance_name" {
  description = "Name tag "
  type        = string
  default     = "TestInstance"
}


 ```



after defining the infrastructure you need inside of .tf files

run :

1. terraform init
to initialise terraform inside that folder and download the provider

```
 terraform init
 
```
2. use terraform plan to see what changes will be made before applying
use terraform apply to apply the configuration

 ```
 terraform plan
 
 terraform apply

```

3. use terraform destroy to take down the configuration

```

terraform destroy
```

