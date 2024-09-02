# 💻Cloud-Security-Project-using-AWS-IAM☁️

Hi! Welcome to my repository containing my AWS Project I've have undertaken on my Cloud joruney⚡️:

In this repository you will see a description of the project, high level architecture, any scripting files that may be relevant to the project and information on other key assets that I have used to develop this project as part of my portfolio.


## **Project Overview**
This  project demonstatres how I have effecitvely used AWS Identity and Access Management (IAM) to control who is authenticated (signed in) and authorised (has permissions) to use AWS account's resources. The requires architectures resources and assets are listed below to complete this project.

<img width="1298" alt="Cloud Security With AWS IAM High Level Architectural Diagram" src="https://github.com/user-attachments/assets/f0683cd6-f204-41fa-acaf-50a0c7f39738">

## **Architecture**

1. **EC2 Instances:** 
2. **IAM Policies:**
3. **IAM User Groups and Users:**
4. **AWS Alias Account:**


## **Deployment Steps**

### Configure EC2 Instances 
1. Launch EC2 Instances with Tags by going to the AWS Management console
2. Select EC2, chose the desired region and select launch Instance
3. Entered the desired name for your EC2 Instance
4. Select 'Additional Tags,' choose 'Add New Tag' and for the Tag information use Key: 'Env' and Value: 'Production'
5. I am using Tags as they are like labels I can attach to AWS resources for organisation. In this case, I creating a tag called 'Env' with a value of 'Production' or 'Development' to label the instances used in production vs development environments. This tagging helps us with identifying all resources with the same tag at once (they are useful filters when you're searching for something), cost allocation, and applying policies based on environment types

<img width="789" alt="EC2 Name Tags Configuration" src="https://github.com/user-attachments/assets/eaf82a14-1db2-4287-acb8-30463b68d961">

6. Head on down to see your EC2 settings and make sure the Amazon Machine Image (AMI) is using a Free tier eligible option. AMI stands for Amazon Machine Image, and it's very similar to those pre-built computers. An AMI is a template or blueprint used to create EC2 instances and contains the operating system along with the applications needed to launch the instance.
Free tier eligible AMIs are those that qualify for the AWS Free Tier, so you won't get charged for using it.
7. For the instance type, also make sure you're using a Free tier eligible option. If AMIs provides pre-built software and operating systems, instance types cover the 'hardware' components such as CPU power, memory size, storage space. So, while the AMI decides what operating system the server runs, the instance type determines how fast and powerful it performs.
8. For Key Pair (login), select Proceed without a key pair.
9. Select Launch instance once the setting above have been correctly configured.
10. We skipped configuring network and storage settings for simplicity in this project. These settings are crucial for fine-tuning your EC2 instances' performance, security, and connectivity, but for this project, we'll focus on the basic steps of launching instances with minimal configuration. Network settings define how the instances interact with the internet and other AWS resources, determining factors like IP addresses and network routing. Storage settings involve choosing the type and size of storage volumes (like hard drives) that your EC2 instance will use to store data.
11. Now create one more EC2 instance for the development environment Repeat the same flow, but this time using these tags Name: 'nextwork-development-yourname' and Env: 'development'
12. Launch your second instance. If you only see one instance on your page, make sure to use that refresh button!

### Create an IAM Policy
1. IAM stands for Identity and Access Management. I will use AWS IAM to manage the access level that other users and services have to resources.
2. To configure IAM Policy, Head to the IAM console.
3. On the left-hand navigation panel of your IAM console, choose Policies. IAM policy is a rule for who can do what with AWS resources. It's all about giving permissions to IAM users, groups, or roles, saying what they can or can't do on certain resources, and when those rules kick in.
4. Choose Create policy.
5. Switch your Policy editor tab to JSON.
6. Here's the policy below. Paste this policy into the editor replacing ALL of the existing code in your editor. This is also saved as IAM JSON file Script.txt in this repository folder.
```bash
    {    
  "Version": "2012-10-17",    
  "Statement": [        
    {            
      "Effect": "Allow",            
      "Action": "ec2:*",            
      "Resource": "*",            
      "Condition": {                
        "StringEquals": {                    
          "ec2:ResourceTag/Env": "development"                
        }            
      }        
    },        
    {            
      "Effect": "Allow",            
      "Action": "ec2:Describe*",            
      "Resource": "*"        
    },        
    {            
      "Effect": "Deny",            
      "Action": [                
        "ec2:DeleteTags",                
        "ec2:CreateTags"            
      ],            
      "Resource": "*"        
    }    
  ] 
}
```

7. Select Next and fill in the policy details:
   Name: NextWorkDevEnvironmentPolicy
   Description: IAM Policy for NextWork's development environment.
8. Once the details above have been entered, select Create policy

### Create an AWS Account Alias
1. Head to the IAM dashboard. In the right-hand side of the dashboard, choose Create under Account Alias.
2. In the Preferred alias field, enter nextwork-alias-yourname. Replace 'yourname' with your name.
3. Select Create Alias. Once created a URL will be provided along with the new account Alias. 

### Create IAM Users and User Groups
1. Choose User groups in your left-hand navigation panel then Choose Group to create the first user group.
2. To set up the group give the user grame name: 'nextwork-dev-group' and attach permission policies: 'NextWorkDevEnvironmentPolicy'
3. Once the steps have been completed, select 'Create user group.'
4. Choose Users from the left-hand navigation panel and choose 'Create user.'
5. Under User name, enter nextwork-dev-yourname.
6. Tick the checkbox for Provide user access to the AWS Management Console.
7. Uncheck the tick box for Users must create a new password at next sign-in.
8. Select 'Next'. To set permissions for your user, we'll simply add it to the user group you've created. Select the checkbox next to nextwork-dev-group. Select 'Next' and select 'Create user'.

### Test User Access
1. Copy the Console sign-in URL
2. Open a new incognito window on your browser.
3. Open the new console sign-in URL in your incognito window.
4. Using the User name and Console password given in your IAM tab,log in.
5. As a new user, you'll notice that some of your dashboard panels are showing 
 already.
6. Head to your EC2 console, and make sure you're in the same Region as the one where you deployed your two production and development instances.
7. Head to Instances.
8. Select your 'production' instance, and in the 'Actions' dropdown, select 'Manage instance state'.
9. Let's try to stop this instance. Select the 'Stop option', then 'Change state'.
10. Select 'Stop'.
11. At the top of your page, you may see a banner that states we've failed to stop this instance. The banner tells us it's because we're not authorised. We don't have permission to stop any instance with the production tag.
12. To stop the instance, head back to the Instances page, and select the checkbox next to nextwork-development-yourname
13. Under the Actions drop-down, select 'Manage instance state' Select Stop, then Change state. Select Stop.
 




## **IAM Policy Simulator**
1. The IAM Policy Simulator lets you test and validate your policies without affecting your actual AWS resources.
2. Head back to your main AWS account.
3. In the IAM dashboard, look for the Policy Simulator link under the Tools panel.
4. Select your dev user group.
5.  Under the Select service drop-down, select EC2.
15. Under the Select actions drop-down, select DeleteTags and StopInstances.
16. Select Run Simulation when you're ready.
17. You'll see that both are denied.
18. Expand the toggle for DeleteTags, and select Show statement.
19. Expand the StopInstances toggle, and in the Instance field, add development to indicate that you want to run the simulation for the instances with that tag.
20. Select Run simulation again.

![image](https://github.com/user-attachments/assets/1b67bf3b-2460-46eb-8c2c-72ea40920bee)

21. Now your Policy Simulator tells you that access is granted after all.


  
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

- **Enhanced Security:** I addressed the issue of unsecured access by implementing fine-grained IAM policies that ensure only authorized users can access specific AWS resources.
- **Access Management:** I resolved the challenge of managing user access by setting up IAM roles and groups, streamlining permission assignment across different teams.
- **Compliance:** I tackled the problem of ensuring compliance with security best practices by enforcing strong password policies, Multi-Factor Authentication (MFA), and regular audits of access logs.
  

## **What issues did I face while working on the project and how did I resolve that issue?**

- **Permission Errors:** I encountered issues with insufficient permissions when trying to execute certain AWS actions. I resolved this by carefully reviewing and adjusting IAM -policies to include the necessary actions.
- **Complex Policy Management:** Managing multiple policies for different users was initially confusing. I overcame this by using policy inheritance and organizing users into groups, -allowing for more efficient policy management.
- **Resource Access Conflicts:** There were conflicts between different IAM policies, leading to unexpected access denials. I resolved this by decoding authorization failure messages and refining policy conditions to avoid overlaps.

 ## **What overall lessons did I learn?**

 - **IAM Management and Best Practice:** As part ot IAM Management best practice, I identified that it is not recommended to user a root account for cloud environment creation. Going forward, I increased the acess robustness of my root using account by regularly changing  passwords, using MFA (Mult Factor Authentication), removing access keys to the root account and reducing overall root user account user for sercurity perposes.

-  **IAM User Creation and Best Practice:** Through doing this project, I also identified that going forward, best practice would be to create a new IAM user for myself and only grant required access also setting up a MFA for the new user making this the primary use account going forward. This is not only best practice, but permits the use of defining a boundary of services that I only want to use. For example, am IAM user cannot be charged for a NAT Gateway, if they don't have permissions to configure one in the first place.

-  **Importance of Principle of Least Privilege:** I learned that applying the principle of least privilege is crucial in minimizing security risks, ensuring users only have the permissions they absolutely need.
  
-  **Value of Clear Documentation:** Documenting IAM policies and access rules thoroughly is essential for maintaining clarity and avoiding future issues.
  
- **Need for Regular Audits:** Regularly auditing IAM configurations helps catch potential security gaps early, ensuring continuous compliance with security standards.
  
