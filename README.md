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

# Jenkins Setup Process

## Installing Jenkins and Configuring SSH

Once the servers were created using Terraform, Jenkins was installed on one of the instances. The following steps were taken:

1. **Jenkins Installation:**
   - Installed Jenkins on the designated instance created by Terraform.

2. **User Login and SSH Key Generation:**
   - Created a Jenkins password and logged in to the Jenkins user through the command line.
   - Generated an SSH key within the Jenkins user environment.

3. **SSH Setup:**
   - Used the generated SSH key to establish an SSH connection to the second server created by Terraform.
   - Tested the SSH connection to ensure successful communication between servers.

4. **SSH Key Sharing:**
   - Copied the public key contents from the first instance and pasted it into the `authorized_keys` file of the second instance.
   - This setup allowed SSH access from the first instance to the second instance.

5. **Python and Virtual Environment Installation:**
   - Installed specific Python versions and set up virtual environments for both the Jenkins user and the Ubuntu user on the first instance.
   - Repeated the same process on the second instance.

# Jenkinsfiles Setup

## SSH and File Transfer Commands

Once everything was setup, I went on to create a command that will ssh into the second server and download the required script for those files. I used a series of scp and ssh commands to execute this. 

```bash
# SSH into the second server and execute the setup script remotely
ssh ubuntu@"ip_address" 'bash -s < /home/ubuntu/setup.sh'

scp /var/lib/jenkins/workspace/setup2.sh ubuntu@ip_address:/home/ubuntu
```

# Jenkins Pipeline Setup

Within Jenkins, a multibranch pipeline was set up using GitHub credentials. The following steps were taken in the Jenkins pipeline configuration:

1. **Multibranch Pipeline Creation:**
   - Configured a multibranch pipeline in Jenkins, linking it to the GitHub repository containing the project.

2. **Pipeline Execution:**
   - Ran the `Jenkinsfilev1` in the multibranch pipeline configuration.
   - The pipeline executed all necessary stages, including testing, building, and deploying the application.

3. **Deployment to Second Instance:**
   - Upon successful completion of the pipeline stages, the application was deployed on the second instance created in the infrastructure setup.

<img width="800" alt="Screenshot 2023-10-13 at 11 04 51 PM" src="https://github.com/Jmo-101/tf_bank/assets/138607757/84a1e46d-8512-4968-9f56-e53d4db6e46a">

<img width="800" alt="Screenshot 2023-10-13 at 11 04 17 PM" src="https://github.com/Jmo-101/tf_bank/assets/138607757/9e603024-b1d2-461d-9f3e-b51493dea512">

# Jenkinsfilev2:
- I decided to make a change to the HTML file, I made a tiny change to the title of the welcome screen of the app and then ran Jenkinsfilev2 with it. Once it ran and deployed successfully, I went on to check the application in the second instance and the HTML change appeared.

<img width="700" alt="Screenshot 2023-10-14 at 12 05 10 AM" src="https://github.com/Jmo-101/tf_bank_app/assets/138607757/9026a80c-6636-401e-9865-54467cb3d12c">

<img width="700" alt="Screenshot 2023-10-14 at 12 04 16 AM" src="https://github.com/Jmo-101/tf_bank_app/assets/138607757/1cc064e3-8154-4bf9-9c80-da0f64dcb737">


