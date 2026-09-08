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