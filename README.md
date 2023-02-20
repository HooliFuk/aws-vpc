# aws-vpc
Find the error and fix it 

terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.0"
    }
  }
}

provider "aws" {
  region = "af-south-1"
}
resource "aws_instance" "web" {
  ami           = "ami-020ae3a2e1e9ac55b"
  instance_type = "t3.micro"
count = 5
  tags = {
    Name = "cloud-Tech"
  }
}

resource "aws_vpc" "svc" {
  cidr_block       = "10.0.0.0/16"
  instance_tenancy = "default"

  tags = {
    Name = "Cloud_Tech"
  }
}

resource "aws_subnet" "PublicSubnet" {
  vpc_id = aws_vpc.svc.id
  cidr_block = "10.0.1.0/24"
}

resource "aws_subnet" "PrivateSubnet" {
  vpc_id = aws_vpc.svc.id
  cidr_block = "10.0.2.0/24"
 }
