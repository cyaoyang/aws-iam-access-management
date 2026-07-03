# AWS IAM Access Management

## Project Overview

This project demonstrates the implementation of secure Identity and Access Management (IAM) within Amazon Web Services (AWS). It covers the creation of IAM users, implementation of Multi-Factor Authentication (MFA), application of the Principle of Least Privilege, and the design of Role-Based Access Control (RBAC) using IAM roles and policies.

The project simulates how organizations manage user identities and permissions to protect cloud resources while ensuring users have only the access required for their responsibilities.

---

## Objectives

This project was completed to:

- Create IAM users
- Configure secure authentication using MFA
- Apply the Principle of Least Privilege
- Design Role-Based Access Control (RBAC)
- Create and assign IAM roles
- Define custom permission policies
- Validate user permissions and access boundaries

---

## AWS Services Used

- AWS Identity and Access Management (IAM)

---

## Security Concepts Demonstrated

- Identity and Access Management
- Authentication vs Authorization
- Principle of Least Privilege
- Multi-Factor Authentication (MFA)
- Role-Based Access Control (RBAC)
- IAM Roles
- IAM Policies
- Permission Boundaries

---

## Architecture


```
                AWS Account
                     │
          ┌──────────┴──────────┐
          │                     │
     IAM Users             IAM Roles
          │                     │
          ├──────────┐          │
          │          │          │
      Admin      Developer   Auditor
          │          │          │
          └──────────┴──────────┘
                     │
             IAM Policies
                     │
             AWS Resources
```

---

## Implementation

### Part 1 – IAM User Management

- Created IAM users
- Assigned least privilege permissions
- Enabled Multi-Factor Authentication (MFA)
- Tested user login

### Part 2 – Role-Based Access Control (RBAC)

- Created Admin role
- Created Developer role
- Created Auditor role
- Defined IAM policies
- Assigned users to appropriate roles
- Validated permission boundaries

---

## Security Best Practices

This project follows several AWS security best practices:

- Avoid using the root account for daily administration
- Enable MFA for privileged users
- Apply the Principle of Least Privilege
- Use IAM roles instead of long-term credentials where possible
- Regularly review IAM permissions
- Separate responsibilities through Role-Based Access Control

---

## Screenshots

Include screenshots of:

- IAM Dashboard
- IAM User Creation
- IAM Policies
- IAM Roles
- Admin Role
- Developer Role
- Auditor Role
- MFA Configuration
- Permission Boundary
- Successful Login Test

---

## Challenges Encountered

One challenge during this project was understanding how IAM policies interact with users and roles. Testing different permission levels highlighted the importance of assigning only the permissions required for each role while avoiding excessive privileges.

---

## Lessons Learned

This project reinforced that Identity and Access Management is one of the most critical security services within AWS. Properly configured IAM users, roles, policies, and MFA significantly reduce the risk of unauthorized access and help organizations implement secure access controls.

---

## Real-World Application

Organizations rely on IAM to securely manage employee access to cloud resources. Implementing Role-Based Access Control (RBAC) and enforcing least privilege ensures that administrators, developers, and auditors receive only the permissions necessary to perform their duties. This approach reduces the attack surface, supports compliance requirements, and strengthens overall cloud security.

---

## Skills Demonstrated

- AWS IAM
- User Management
- IAM Roles
- IAM Policies
- Role-Based Access Control (RBAC)
- Least Privilege
- Multi-Factor Authentication (MFA)
- Permission Boundaries
- Cloud Security

## Future enhancements for this project include:

- Integrate IAM Identity Center (AWS IAM Identity Center) for centralized workforce authentication.
- Enforce MFA for all users through account policies.
- Apply Attribute-Based Access Control (ABAC) using tags.
- Monitor IAM activity with AWS CloudTrail and Amazon CloudWatch.
- Regularly audit permissions using IAM Access Analyzer.
