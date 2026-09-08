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
```

This architecture separates public-facing resources from private internal resources. Users access the application through the CDN and load balancer, while the application servers and database remain protected from direct Internet access.

## CDN

The Content Delivery Network (CDN) delivers cached copies of static content such as HTML, CSS, JavaScript, and images from locations closer to users. This improves loading speed and reduces unnecessary traffic reaching the application servers.

## Load Balancer

The load balancer receives incoming application requests and distributes them across available application servers. This helps prevent one server from handling all traffic and improves the application's availability and reliability.

## Application Servers

The application servers process requests from users and handle the application's business logic. They should be placed in a private network or private subnet so Internet users cannot connect to them directly. Only approved traffic from the load balancer should be allowed to reach the application servers.

## Database

The database stores student records and other application data. It should remain private and should never be directly accessible from the Internet. Only authorized application servers should be allowed to communicate with the database.

---

# Public and Private Resources

| Resource | Public or Private? | Explanation |
|---|---|---|
| CDN | Public | The CDN must be reachable by users because it delivers application content to users over the Internet. |
| Load Balancer | Public | The Internet-facing load balancer receives approved incoming traffic and forwards requests to the private application servers. |
| Application Server | Private | Application servers should not be directly exposed to the Internet and should only accept application traffic from the load balancer. |
| Database | Private | The database contains student information and should only accept connections from authorized application servers. |

---

# Security Controls

## IAM

Identity and Access Management (IAM) should control who can access the cloud environment and what actions each user is allowed to perform. Permissions should be based on job responsibilities instead of giving every user full administrative privileges. Only authorized administrators should be allowed to manage sensitive cloud resources and security settings.

## MFA

Multi-Factor Authentication (MFA) should be required for administrator accounts and other accounts that have access to sensitive systems or data. MFA provides an additional layer of protection because a stolen password alone would not be enough to access the account. This helps reduce the risk of unauthorized access caused by compromised credentials.

## Firewall / Security Group

Firewall or security group rules should allow only the connections necessary for the application to operate.

```text
Internet → Load Balancer = Allowed
Load Balancer → Application Servers = Allowed
Application Servers → Database = Allowed

Internet → Application Servers = Blocked
Internet → Database = Blocked
```

These rules prevent Internet users from bypassing the public entry point and directly accessing internal application servers or the database.

## Encryption

Student information should be encrypted both while it is being transmitted and while it is stored. Encryption protects sensitive information from being easily read if network traffic is intercepted or stored data is accessed without authorization. HTTPS/TLS can protect data in transit, while storage encryption can protect data at rest.

## Logging

The system should record important activities such as successful and failed login attempts, administrative actions, permission changes, application errors, and access to sensitive resources. Logs provide information that can be reviewed when troubleshooting problems or investigating security incidents.

## Monitoring

Monitoring should be used to identify suspicious activity such as repeated failed login attempts, unusual network traffic, unexpected access attempts, or abnormal application behavior. Administrators should receive alerts when potentially dangerous activity is detected so they can investigate and respond quickly.

## Backup

The database should have regular backups so student information can be recovered if data is accidentally deleted, corrupted, lost because of a system failure, or affected by a security incident. Backups should also be protected from unauthorized access and tested periodically to confirm that the data can be restored.

---

# Principle of Least Privilege

The Principle of Least Privilege means that each user should receive only the permissions necessary to perform their assigned responsibilities.

| User | Allowed Access |
|---|---|
| Administrator | Manage system configuration, user accounts, permissions, security settings, and other authorized administrative functions. |
| Instructor | View student records related to assigned classes and update authorized academic information when necessary. |
| Student | View only their own authorized student information and account details. |
| Developer | Access application code, development tools, logs needed for troubleshooting, and approved development resources without unrestricted access to production student data. |

Administrator privileges should not be given to every user because unnecessary access increases the risk of accidental changes, misuse, and security incidents.

---

# Shared Responsibility Model

| Responsibility | Cloud Provider or Customer? |
|---|---|
| Physical data center | Cloud Provider |
| Physical servers | Cloud Provider |
| User accounts | Customer |
| Student data | Customer |
| IAM permissions | Customer |
| Application security | Customer |
| Database access rules | Customer |
| Backups | Customer |

## 1. What does Security OF the Cloud mean?

Security **OF the Cloud** refers to the responsibilities handled by the cloud provider. These responsibilities include protecting physical data centers, physical servers, networking infrastructure, and the underlying systems used to provide cloud services.

## 2. What does Security IN the Cloud mean?

Security **IN the Cloud** refers to the customer's responsibility for securely configuring and using cloud resources. This includes managing user accounts, IAM permissions, application security, student data, database access rules, and backups.

---

# Architecture Questions

## 3. Which resource should be directly accessible from the Internet?

The public-facing components, such as the CDN and Internet-facing load balancer, should be accessible from the Internet. The application servers and database should remain private so unnecessary resources are not directly exposed to external users.

## 4. Why should the database remain private?

The database contains student information that should not be directly exposed to Internet users. Keeping it private reduces the risk of unauthorized access and ensures that only approved application servers can communicate with it.

## 5. Why should users not connect directly to the database?

Users should access student information through the application instead of directly connecting to the database. The application can authenticate users, validate requests, and enforce access permissions before retrieving or changing data. Direct database access could bypass these security controls.

## 6. What is the purpose of a load balancer?

A load balancer distributes incoming requests across multiple application servers. This prevents one server from handling all of the traffic and helps improve performance, reliability, and availability.

## 7. What happens if one application server fails?

If one application server fails, the load balancer can redirect requests to another healthy application server. This allows the application to continue operating and reduces the impact of a single server failure.

## 8. What is the purpose of a CDN?

A CDN delivers cached static content from locations closer to users. This helps improve loading speed, reduce latency, and decrease the amount of traffic that reaches the main application infrastructure.

## 9. Why should administrator accounts use MFA?

Administrator accounts have powerful permissions and can make important security and configuration changes. MFA adds another verification factor so a stolen password alone is not enough to gain administrative access. This provides stronger protection against account compromise.

## 10. Why should administrator access not be given to every employee?

Most employees do not need full administrator privileges to perform their responsibilities. Giving unnecessary administrative access increases the risk of accidental changes, misuse, and serious damage if an account is compromised. Permissions should instead be assigned according to each person's job responsibilities.

## 11. Why are logging and monitoring important?

Logging records important activities and system events, while monitoring helps identify unusual or suspicious behavior. Together, they help administrators troubleshoot problems, investigate security incidents, and respond to threats more quickly.

## 12. Why are backups important?

Backups allow important student information to be restored if data is accidentally deleted, corrupted, lost, or affected by a security incident. Reliable and regularly tested backups improve system recovery and help the organization continue operating after a failure.