# **The Process of Orchestrating Amazon EC2 using Terraform -  Samarth M Katageri**

---

With this document, I am covering the details of 2 actions:
1. How to launch EC2 instance manually
2. How to orchestrate Amazon EC2 to launch an instance automatically using Terraform by HashiCorp Language.

---

## 1. How to launch EC2 instance manually?

Pre-requisites you should have:
1. AWS account with your own IAM user privilege, not in root user access.
2. IAM policy not set to *AdministratorAccess* as it leads to hacking your AWS account itself.

**Steps to launch EC2 instance**:

1. Once you logged into your AWS IAM user account and met with AWS Management Console, search for "EC2" service.
2. When you see "EC2" Dashboard, click on "Launch Instance" button, or else if you meet with "Instances" tab from the left panel, click on "Launch Instance" button on the top-right corner. You will meet with a page for creating an instance.
3. You can choose which operating system image you like, with the reason all these OSes are called as Amazon Machine Images (AMI) (for example, Amazon Linux 2).
    - Before proceeding with instance details, ensure you have a Virtual Private Cloud (VPC) configured. Search for "VPC" service in the console.
    - Create a VPC by clicking "Create VPC", choosing "VPC and more" to automatically generate subnets, route tables, and an internet gateway. This provides the isolated network space where your EC2 will reside.
    - Back in the EC2 launch page, under "Network settings", select the VPC and the specific Subnet you just created.
    - Ensure "Auto-assign public IP" is enabled if you need to access it from the internet.
    - After you choose one AMI, choose any instance types, which meets Free-tier eligibility (for example, t2.micro).
    - After you choose the instance type, choose a key pair if you already have one, or create the key pair as it needs to login through EC2 instance.
    - After the key pair, choose your security group that contains such essential port allowances:
        * Port 80 - HTTP
        * Port 22 - SSH (if it's Unix-based AMI), Port 3389 - RDP (if it's Windows-based AMI) or Port 5900 - VNC (if it's MacGUI AMI)
      If you don't have existing security group, create a new one.
4. After all these steps, see the right-side panel for instance-briefing, and click the "Launch Instance" button.

There you go, you launched an instance using AWS WebGUI (or technically, manually).

Here is the video tutorial of how you can launch EC2 instance manually:

<!-- Video Tutorial -->
Drive link: [How to setup VPC & EC2 manually?](https://drive.google.com/file/d/1Rzc06pHMtZgoojzShiOpOPij2CxHTT6B/view?usp=sharing)

---

## 2. How to orchestrate Amazon EC2 to launch an EC2 instance automatically using Terraform?

Pre-requisites you should have:
1. AWS account with your own IAM user privilege, not in root user access.
2. IAM policy not set to *AdministratorAccess* as it leads to hacking your AWS account itself.
3. Access Key associated with your AWS IAM user account, giving privilege to orchestrate outside of AWS WebGUI.
4. Terraform installed locally.

**Steps to launch EC2 instance using Terraform**:

1. Open AWS Management Console, and search for "EC2" service.
2. When you see "EC2" Dashboard, go to "Instances" tab when clicked from the left panel.
3. Keep it open and minimize the browser window to open any IDE (e.g., Visual Studio Code) locally in your computer.
4. Make a folder and create directories for Terraform scripting.
5. Create a file named `main.tf` and define the provider and resources. You must first define the `aws_vpc` resource to create the network space, followed by an `aws_subnet` associated with that VPC.
6. Within the same `main.tf`, define the `aws_instance` resource. Ensure you reference the subnet ID from the VPC resource you defined earlier (e.g., `subnet_id = aws_subnet.main.id`) to ensure the instance is launched within your custom network.
7. Open your terminal in the IDE, and run the following commands:
    - `terraform init` to initialize the directory and download the AWS provider.
    - `terraform plan` to preview the infrastructure changes (VPC, Subnet, and EC2).
    - `terraform apply` to execute the orchestration and launch the services automatically.

By referencing the `main.tf` logic, Terraform handles the dependency mapping, ensuring the VPC is ready before the EC2 instance attempts to launch.

There you go, you orchestrated AWS services using Terraform.

Here is the video tutorial of how you can launch EC2 instance using Terraform:

<!-- Video Tutorial -->
Drive Link: [How to orchestrate AWS Services using Terraform?](https://drive.google.com/file/d/1FMYp1mlC0_NaYUUlEXO4sEoz446R2SOD/view?usp=sharing)

---

**Author:** Samarth M Katageri  
**License:** None
**Date:** 03-02-2026
