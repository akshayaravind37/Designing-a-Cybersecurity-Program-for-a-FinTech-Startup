# Designing-a-Cybersecurity-Program-for-a-FinTech-Startup
Comprehensive cybersecurity program and secure technical architecture designed for a FinTech startup. This repository includes logical network segmentation, a STRIDE threat model, a 5x5 risk register, an IAM least-privilege role model, Splunk SIEM detection rules, and an incident response playbook.  
Team Members (Group 1)
- Remi Adekunle
- Akshay Aravind
- Cortland Brown
- Sabrina Tan

Repository Structure
This repository contains the complete documentation for our security architecture, threat models, risk assessment, and incident response plans:

- System Architecture.jpg: High-level architectural diagram of the FinTech environment.
- SIEM_DETECTIONS.md: Splunk monitoring strategies and SPL queries for threat detection.
- Group 1 - Final Project.pdf: The complete consolidated project report including STRIDE threat model, Risk Register, IAM Least-Privilege Design, and Incident Response Workflow.

System Architecture Highlights
Our FinTech environment relies on principles of defense-in-depth, least-privilege access, and security-by-design. The architecture is divided into clearly defined zones to reduce the attack surface:
- Public Zone: Point of entry for all external traffic. Includes DNS, CDN, DDoS protection, Web Application Firewall (WAF), and API Gateway to filter requests.
- Application Zone: Processes business logic and transaction processing. Identity provider integrates OIDC/SAML-based authentication and enforces MFA. Separated from the Public Zone by a DMZ boundary.
- Data Zone: Contains the primary transaction database, read replica, encrypted object storage, and KMS/Secrets manager. Access is highly restricted via firewall rules permitting only application-layer access.
- Management Zone: Allows administrators to securely connect through a bastion host requiring MFA and session recording, establishing a Privileged Access Boundary (PAB).
- Monitoring Zone: Provides centralized logging and alerting from the SIEM.

All communications utilize secure protocols (HTTPS, TLS, mTLS, SSH) to provide confidentiality, integrity, and authentication.

Incident Response
Our six-step process for responding to a security incident:
1. Detect: Monitor our environment using SIEM dashboards, VPC flow logs, and IAM logs.
2. Analyze: Determine if the threat is inside the critical data zone or restricted to public networks.
3. Contain: Isolate EC2 instances, block bad IPs at the firewall/WAF, or disable compromised accounts.
4. Eradicate: Delete infected files, fix exploited vulnerabilities, and delete access keys.
5. Recover: Restore affected systems to normal functioning using known clean off-site backups.
6. Lessons Learned: Conduct a postmortem analysis to document the response, update SIEM detection rules, and update the Risk Register.
