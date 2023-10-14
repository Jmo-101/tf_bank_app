<p align="center">
<img src="https://github.com/kura-labs-org/kuralabs_deployment_1/blob/main/Kuralogo.png">
</p>
<h1 align="center">Terraform-retail-banking<h1> 

#Planning

<img width="600" alt="Screenshot 2023-10-14 at 12 25 14 AM" src="https://github.com/Jmo-101/tf_bank/assets/138607757/64f1182f-e76c-48d9-ba5d-edaa62e1cdb1">

# Purpose

## Purpose
This project showcases the use of Terraform to create two instances within a VPC in two different availability zones and subnets. With the use of Git commands in the command line, I was able to upload it to a GitHub repository and link it to a Jenkins pipeline in order to build, test, and deploy the application.

# Terraform Deployment Process

## Main Configuration Files

### `main.tf`
Within Terraform, a `main.tf` file was created to define the necessary resource blocks for the deployment. The following resource blocks were included:

- **VPC:** Defines the Virtual Private Cloud (VPC) to isolate the network environment.
- **Subnet:** Specifies the subnets within the VPC.
- **AWS Instance:** Sets up the AWS instances within the defined subnets.
- **Internet Gateway:** Establishes an Internet Gateway for connecting the VPC to the internet.
- **Routing Table:** Configures the routing table for the VPC.
- **Availability Zone:** Specifies the availability zones for distributing resources.
- **Security Groups:** Defines security groups for controlling inbound and outbound traffic.

### `variables.tf`
Additionally, a `variables.tf` file was created to store sensitive variables that should not be publicly known.
