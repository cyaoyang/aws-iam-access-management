# AWS IAM Access Management

## Executive Summary

This project demonstrates the implementation of secure Identity and Access Management (IAM) within AWS. It focuses on protecting cloud resources by applying the Principle of Least Privilege, implementing Role-Based Access Control (RBAC), enabling Multi-Factor Authentication (MFA), and validating user permissions.

The implementation reflects security practices commonly adopted in enterprise cloud environments.

---

# Business Scenario

A growing technology company has recently migrated its infrastructure to AWS.

As the number of employees increases, managing access using the root account is no longer secure or scalable.

The company requires an IAM solution that:

- Separates administrative responsibilities
- Restricts developer access
- Provides auditors with read-only visibility
- Protects privileged accounts using MFA
- Follows the Principle of Least Privilege

As the Cloud Security Engineer, your task is to design and implement this solution.

---

# Project Objectives

- Create IAM users
- Create IAM roles
- Configure RBAC
- Apply Least Privilege
- Enable MFA
- Validate permissions

---

# AWS Services Used

| Service      | Purpose               |
|--------------|-----------------------|
| IAM          | Identity Management   |
| MFA          | Secure Authentication |
| IAM Policies | Authorization         |
| IAM Roles    | RBAC                  |

---

# Architecture Diagram

<img width="776" height="681" alt="image" src="https://github.com/user-attachments/assets/2a7ad598-0c57-474b-b20a-5a4afe89670e" />



---

# Solution Design

## IAM Users

| User    | Role         |
|---------|--------------|
| Alice   | Administrator|
| Bob     | Developer    |
| Charlie | Auditor      |

---

## IAM Roles

| Role          | Permissions           |
|---------------|-----------------------|
| Administrator | Full Access           |
| Developer     | Development Resources |
| Auditor       | Read Only             |

---

## Permission Model

The permission model for this project was designed following the **Principle of Least Privilege (PoLP)** and **Role-Based Access Control (RBAC)**.

Three IAM users were created to represent common organizational roles:

- **Administrator**
- **Developer**
- **Auditor**

To simplify permission management and demonstrate RBAC, each user was assigned to a corresponding IAM group:

- **Admin-Group**
- **Developer-Group**
- **Auditor-Group**

Permissions were assigned to the IAM groups rather than directly to individual users. This approach simplifies administration, improves scalability, and ensures users with the same job responsibilities inherit a consistent set of permissions.

Each role was granted only the permissions required to perform its responsibilities, reducing the attack surface and minimizing the risk of unauthorized access or accidental changes to AWS resources.

### Administrator

The **Administrator** user was granted the **AdministratorAccess** managed policy to simulate a cloud administrator responsible for managing the AWS environment. This role has unrestricted access to AWS resources, including Identity and Access Management (IAM), compute, storage, networking, and security services.

Because this is a highly privileged role, it should always be protected with **Multi-Factor Authentication (MFA)** and should only be used when administrative tasks are required.

### Developer

The **Developer** user was granted permissions to:

- Amazon EC2 – Full Access
- Amazon S3 – Full Access
- Amazon CloudWatch Logs – Read Only

This permission set enables developers to deploy and manage application resources while preventing them from modifying IAM configurations or other security-critical settings. By limiting administrative privileges, the organization reduces the risk of accidental or malicious changes to the AWS environment.

### Auditor

The **Auditor** user was granted read-only permissions to:

- IAM
- Amazon EC2
- Amazon S3
- AWS CloudTrail
- Amazon CloudWatch
- AWS Config

These permissions allow auditors to review security configurations, monitor resource usage, examine audit logs, and verify compliance without the ability to modify or delete AWS resources. Read-only access preserves the integrity of the environment while supporting governance and security auditing activities.

### Security Principles Applied

This permission model demonstrates several core cloud security principles:

- **Principle of Least Privilege (PoLP):** Users receive only the permissions necessary to perform their assigned duties.
- **Role-Based Access Control (RBAC):** Permissions are assigned based on job responsibilities rather than individual users.

---

# Implementation

## Step 1 — Create IAM Users

### Why?

Creating individual IAM users instead of using the AWS root account improves accountability by ensuring that every action can be traced back to a specific user (non-repudiation). It also strengthens security by reducing the use of the highly privileged root account for day-to-day administrative tasks. 

### Screenshot

<img width="761" height="216" alt="image" src="https://github.com/user-attachments/assets/1f6655b9-627f-4781-9ba8-ab21a034a581" />


### Security Consideration

* Every individual should have their own identity in the AWS cloud.

* Every priveleged account should be secured with multi-factor authentication (MFA).

* Each account should be secured a strong password of at least 12 characters in length containing uppercase and lowercase characters and at least one special character.

* The AWS root account should not be used for day-to-day administrative tasks. Instead, administrators should use IAM users or IAM roles with only the permissions required to perform their job functions.

* Permissions should follow the Principle of Least Privilege, granting users only the access necessary to perform their responsibilities.

---

## Step 2 — Configure Least Privilege

* Admin user was placed in admin-group with AdministratorAccess

<img width="1363" height="394" alt="image" src="https://github.com/user-attachments/assets/c5367114-5d0d-45e3-a4ca-1fda04024166" />

<img width="1278" height="427" alt="image" src="https://github.com/user-attachments/assets/9c4c5109-689d-4647-a5ce-8cdce507228f" />

* Developer user was placed in developer-group with AmazonEC2FullAccess, AmazonS3FullAccess and CloudWatchLogsReadOnlyAccess

<img width="1440" height="425" alt="image" src="https://github.com/user-attachments/assets/d6d83545-eb7e-4bc5-b890-3f46659ed959" />

<img width="1284" height="473" alt="image" src="https://github.com/user-attachments/assets/748dc7be-0b47-4b3b-9703-700e31e215c1" />

* Auditor user was placed in auditor-group with AmazonEC2ReadOnlyAccess, AmazonS3ReadOnlyAccess, AWSCloudTrail_ReadOnlyAccess, CloudWatchReadOnlyAccess and IAMReadOnlyAccess.

<img width="1361" height="417" alt="image" src="https://github.com/user-attachments/assets/4482fc23-8d7f-4ded-90ab-6b994a7385b3" />

<img width="1276" height="482" alt="image" src="https://github.com/user-attachments/assets/5db8bdc3-8e24-4425-b74d-43a832aa1f69" />

---

## Step 3 — Enable MFA

* Admin user was configured to perform MFA when logging in.

<img width="1263" height="200" alt="image" src="https://github.com/user-attachments/assets/8f5d7e68-6d2b-4a15-852a-db29ab742cd7" />

---

## Step 4 — Create IAM Roles

### Objective

Create IAM roles to provide temporary, role-based access to AWS resources without relying on long-term credentials. IAM roles improve security by allowing permissions to be assumed only when required and are commonly used by AWS services, applications, and users requiring temporary elevated access.

### Why?

Unlike IAM users, IAM roles do not have permanent credentials. Instead, they are assumed temporarily, reducing the exposure of long-term access keys and supporting the Principle of Least Privilege.

Three IAM roles were created to represent common organizational responsibilities:

| IAM Role | Purpose |
|----------|---------|
| **InfrastructureAdminRole** | Provides administrative access for infrastructure management tasks. |
| **ApplicationDeveloperRole** | Allows developers to deploy and manage application resources while restricting access to security-sensitive services. |
| **SecurityAuditorRole** | Provides read-only access for security reviews, compliance audits, and monitoring activities. |

### Implementation

- Created the **InfrastructureAdminRole**.
- Attached the **AdministratorAccess** policy.
- Created the **ApplicationDeveloperRole**.
- Attached permissions for Amazon EC2, Amazon S3, and Amazon CloudWatch Logs.
- Created the **SecurityAuditorRole**.
- Attached read-only policies for IAM, Amazon EC2, Amazon S3, AWS CloudTrail, and Amazon CloudWatch.

### Screenshot

<img width="1804" height="630" alt="image" src="https://github.com/user-attachments/assets/73bdf003-90c1-4745-bb5e-100da240a4a5" />


### Security Considerations

- IAM roles provide temporary credentials instead of permanent access keys.
- Role-based permissions reduce the need to assign excessive permissions directly to individual users.
- Separating administrative, development, and auditing roles supports the Principle of Least Privilege and Separation of Duties.
- In production environments, IAM roles are preferred over long-term IAM user credentials whenever possible.

---

## Step 5 — Test Permissions

...

---

# Security Decisions

### Why Least Privilege?

...

### Why RBAC?

...

### Why MFA?

...

### Why Permission Boundaries?

...

---

# Challenges Encountered

Example:

Initially, understanding how IAM policies interact with IAM roles required additional testing. By validating permissions using different user accounts, I gained a clearer understanding of AWS authorization behaviour.

---

# Lessons Learned

This project strengthened my understanding of AWS Identity and Access Management and highlighted how effective access control reduces security risks in cloud environments.

---

# Future Improvements

Future enhancements include:

- AWS IAM Identity Center
- IAM Access Analyzer
- ABAC
- AWS Organizations SCPs
- Automated IAM auditing

---

# Skills Demonstrated

- AWS IAM
- RBAC
- IAM Policies
- MFA
- Least Privilege
- Cloud Security
- Identity Management

---

# References

AWS IAM Documentation

AWS Security Best Practices

NIST Access Control Principles

