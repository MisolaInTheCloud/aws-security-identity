# AWS Security and Identity

This assignment demonstrates core IAM operations using the AWS Console and CLI, including user creation, permission testing, MFA setup, and custom role policies.

---

## 1. IAM User Creation with Restricted Permissions

**Objective:** Create an IAM user with read-only access to Amazon S3.

### 🛠️ Steps

- Created IAM user: testUserM4aceProject
- Assigned managed policy: AmazonS3ReadOnlyAccess

### 📸 Screenshots

- IAM User Creation: <img width="785" alt="image" src="https://github.com/user-attachments/assets/2ae1d29b-9d6c-4b4d-970d-107007701d44" />
- Attach Policy(screenshots/attach-policy.png): : <img width="775" alt="image" src="https://github.com/user-attachments/assets/fba41d71-f100-410b-bdd6-ac9665e3d123" />
- Policy Details(screenshots/policy-details.png):    <img width="772" alt="image" src="https://github.com/user-attachments/assets/bc142481-c8bc-4817-bf93-6143afcc70cc"/>

---

## 2. Testing User Permissions

**Objective:** Verify read-only access to S3 and denied access to other services.

### 🔍 CLI/Console Tests

- ✅ Listed S3 buckets successfully
- ❌ Denied when attempting:
  - Creating an S3 bucket
  - Launching EC2 instances
  - Creating Subnets

### 📸 Screenshots

- ![S3 Bucket Creation Attempt: <img width="775" alt="image" src="https://github.com/user-attachments/assets/5280f227-191b-45e1-81e1-05011f87bdf5"/>
- ![EC2 Launch Attempt: <img width="785" alt="image" src="https://github.com/user-attachments/assets/db24ab4b-c40e-41b2-8ea0-0160b0fe7be3" />
- ![Subnet Creation Attempt: <img width="958" alt="image" src="https://github.com/user-attachments/assets/ec799ab0-107b-4e6c-91ee-ef71ae2ecda0" />

---

## 3. Enabling Multi-Factor Authentication (MFA)

**Objective:** Secure the IAM user with MFA.

### 🛠️ Steps

- Used AWS Console to enable virtual MFA device
- Scanned QR code using authenticator app
- Successfully activated MFA

### 📸 Screenshot

- ![MFA Setup : <img width="859" alt="image" src="https://github.com/user-attachments/assets/901704ff-4352-40e4-9aaf-feaad7176a54" />
<img width="567" alt="image" src="https://github.com/user-attachments/assets/c13d495d-8c35-4fb1-80e7-b0df597724fb" />
<img width="866" alt="image" src="https://github.com/user-attachments/assets/ddabaf67-dc20-4a34-a8b9-155d89ff31f1" />

MFA Required at the point of logging in for the User: 
<img width="297" alt="image" src="https://github.com/user-attachments/assets/c817cc20-cbd7-47e8-b73e-7dd9302af425" />

---

## 4. Creating and Attaching a Custom Policy to an IAM Role

**Objective:** Define a custom IAM policy and attach it to a role with EC2 read-only access.
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

### 🛠️ Policy JSON

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ec2:DescribeInstances",
        "ec2:DescribeVolumes"
      ],
      "Resource": "*"
    }
  ]
}
