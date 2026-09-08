# Secure Cloud Architecture Plan

## Proposed Architecture

The proposed Student Management Application follows this architecture:

```text
Users
  ↓
CDN
  ↓
Load Balancer
  ↓
Application Server 1 / Application Server 2
  ↓
Private Database

---

# Security Controls

## IAM

Identity and Access Management (IAM) should be used to control who can access the cloud environment and what actions each user is allowed to perform. Access should be based on a person's job responsibilities instead of giving every user full administrative privileges. Only authorized administrators should be able to manage sensitive cloud resources and security settings.

## MFA

Multi-Factor Authentication (MFA) should be required for administrator accounts and other accounts with access to sensitive systems or data. MFA provides an additional layer of protection because a stolen password alone would not be enough to access the account. It reduces the risk of unauthorized access caused by compromised credentials.

## Firewall / Security Group

Firewall or security group rules should only allow connections that are necessary for the application to operate.

```text
Internet → Load Balancer = Allowed
Load Balancer → Application Servers = Allowed
Application Servers → Database = Allowed

Internet → Application Servers = Blocked
Internet → Database = Blocked