# Secure Cloud Architecture

## Student Information

Name: David, Ellie Wayne C.  
Section: CCIS-7E  
Course: BSIT - Network Administration  
Date: September 5, 2026  

## Project Description

This activity demonstrates a proposed secure cloud architecture for a Student Management Application. It focuses on cloud networking, public and private resources, security controls, least privilege, and the Shared Responsibility Model.

## Architecture

Users → CDN → Load Balancer → Application Servers → Private Database

The CDN and load balancer handle incoming user traffic, while the application servers and database remain protected from direct Internet access.

## Security Controls

- IAM
- MFA
- Firewall / Security Groups
- Private Subnets
- Encryption
- Logging
- Monitoring
- Backups