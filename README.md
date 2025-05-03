# AWS Security and Identity 

This assignment demonstrates key Identity and Access Management (IAM) operations in AWS using the AWS CLI.

---

## 1. IAM User Creation with Restricted Permissions

### Steps:
1. Create a new IAM user--> User name: "testUserM4aceProject". I logged in to my Root account to create 
   ```bash
      aws iam create-policy --policy-name AmazonS3ReadOnlyAccess \

   <img width="785" alt="image" src="https://github.com/user-attachments/assets/2ae1d29b-9d6c-4b4d-970d-107007701d44" />
   Attached Policies directly: <img width="775" alt="image" src="https://github.com/user-attachments/assets/fba41d71-f100-410b-bdd6-ac9665e3d123" />

   I atached 'Read Only Access for S3':

   <img width="772" alt="image" src="https://github.com/user-attachments/assets/bc142481-c8bc-4817-bf93-6143afcc70cc" />


Tried to create S3 Bucket with the test user and got this response:
<img width="958" alt="image" src="https://github.com/user-attachments/assets/5280f227-191b-45e1-81e1-05011f87bdf5" />

Tried to launch EC2

<img width="945" alt="image" src="https://github.com/user-attachments/assets/db24ab4b-c40e-41b2-8ea0-0160b0fe7be3" />

Tested with creating subnets too but :

<img width="815" alt="image" src="https://github.com/user-attachments/assets/ec799ab0-107b-4e6c-91ee-ef71ae2ecda0" />

Enforced MFA for the user:
<img width="859" alt="image" src="https://github.com/user-attachments/assets/901704ff-4352-40e4-9aaf-feaad7176a54" />

<img width="567" alt="image" src="https://github.com/user-attachments/assets/c13d495d-8c35-4fb1-80e7-b0df597724fb" />

MFA Done: <img width="866" alt="image" src="https://github.com/user-attachments/assets/ddabaf67-dc20-4a34-a8b9-155d89ff31f1" />


Created a new role with access to read ECS only: 
This grants read-only access to Amazon ECR (Elastic Container Registry) across all repositories in the AWS account.

 When to Use This
Use this role/policy when:

A developer, CI/CD tool, or read-only auditor needs access to pull images, view repositories, inspect image tags and scan results.

It does not allow pushing images or modifying any repository configuration.



<img width="898" alt="image" src="https://github.com/user-attachments/assets/8fcfe024-a08b-4e9e-a7d6-a146d4b861aa" />

With this Json Permission: 
<img width="846" alt="image" src="https://github.com/user-attachments/assets/da02a3dd-e6a3-4934-9313-6a1a08e573a2" />


   aws iam create-user --user-name restricted-user
   
aws iam attach-user-policy \
  --user-name restricted-user \
  --policy-arn arn:aws:iam::<account-id>:policy/ReadOnlyAccessPolicy
