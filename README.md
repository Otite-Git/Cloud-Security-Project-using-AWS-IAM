# 💻Cloud-Security-with-AWS-IAM☁️

Hi! Welcome to my repository containing my AWS Project I've have undertaken on my Cloud joruney⚡️:

In this repository you will see a description of the project, high level architecture, any scripting files that may be relevant to the project and information on other key assets that I have used to develop this project as part of my portfolio.


## **WordPress Website Page** TO BE EDITED

[www.luxelimosrentals.com](https://drive.google.com/file/d/1Gy5ZhBRLFuDI_Mi-Fpw_jSVhp-mOQ7mo/view?usp=sharing)


## **Project Overview**
This  project demonstatres how I have effecitvely used AWS Identity and Access Management (IAM) to control who is authenticated (signed in) and authorised (has permissions) to use AWS account's resources. The requires architectures resources and assets are listed below to complete this project.

<img width="1298" alt="Cloud Security With AWS IAM High Level Architectural Diagram" src="https://github.com/user-attachments/assets/f0683cd6-f204-41fa-acaf-50a0c7f39738">

## **Architecture**

1. **EC2 Instances:** 
2. **IAM Policies:**
3. **IAM User Groups and Users:**
4. **AWS Alias Account:**


## **Deployment Steps**

### VPC Setup TO BE EDITED

## **How to Use**

1. Clone this repository to your local machine.
2. Follow the AWS documentation to create the required resources (EC2 Instances, IAM Policies etc.) as outlined in the architecture overview.
3. Use the provided scripts and documentation if provided in the repository to set up the EC2 instances and IAM roles.

## **Additional Resources**

- **AWS Documentation:** Refer to the [AWS documentation](https://aws.amazon.com/documentation/) for detailed guides on setting up VPC, EC2, Auto Scaling, Load Balancer, and other services.
- **GitHub Repository Files:** Refer to [Otite-Git/Host-WorPress](https://github.com/Otite-Git/Cloud-Security-with-AWS-IAM/tree/main) to access the repository files for scripts, architectural diagrams, and configuration files necessary for deploying the website.

## **Contributing**

Contributions to this project are welcome! Please fork the repository and submit a pull request with your enhancements.

## **What problems did I solve by completing this project?**

## **What issues did I face while working on the project and how did I resolve that issue?**

 ## **What overall lessons did I learn?**

 - **IAM Management and Best Practice:** As part ot IAM Management best practice, I identified that it is not recommended to user a root account for cloud environment creation. Going forward, I increased the acess robustness of my root using account by regularly changing  passwords, using MFA (Mult Factor Authentication), removing access keys to the root account and reducing overall root user account user for sercurity perposes.

-  **IAM User Creation and Best Practice:** Through doing this project, I also identified that going forward, best practice would be to create a new IAM user for myself and only grant required access also setting up a MFA for the new user making this the primary use account going forward. This is not only best practice, but permits the use of defining a boundary of services that I only want to use. For example, am IAM user cannot be charged for a NAT Gateway, if they don't have permissions to configure one in the first place. 
  
