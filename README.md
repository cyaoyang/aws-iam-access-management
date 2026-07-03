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

*(AWS architecture diagram here)*

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

*(Explain why permissions were assigned this way.)*

---

# Implementation

## Step 1 — Create IAM Users

### Why?

Creating individual IAM users instead of using the AWS root account improves accountability by ensuring that every action can be traced back to a specific user (non-repudiation). It also strengthens security by reducing the use of the highly privileged root account for day-to-day administrative tasks. 

### Screenshot

<img width="761" height="216" alt="image" src="https://github.com/user-attachments/assets/1f6655b9-627f-4781-9ba8-ab21a034a581" />


### Security Consideration

Every individual should have their own identity in the AWS cloud.

Every priveleged account should be secured with multi-factor authentication (MFA).

Each account should be secured a strong password of at least 12 characters in length containing uppercase and lowercase characters and at least one special character.

The AWS root account should not be used for day-to-day administrative tasks. Instead, administrators should use IAM users or IAM roles with only the permissions required to perform their job functions.

Permissions should follow the Principle of Least Privilege, granting users only the access necessary to perform their responsibilities.

---

## Step 2 — Configure Least Privilege

...

---

## Step 3 — Enable MFA

...

---

## Step 4 — Create IAM Roles

...

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

