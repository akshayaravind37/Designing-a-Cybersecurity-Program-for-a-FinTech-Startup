SIEM Monitoring and Detection Strategy

Data Ingestion
Our monitoring program ingests security event data from identity systems, network infrastructure, applications, endpoints, and data repositories. All security event data is normalized using Splunk's Common Information Model (CIM) to ensure consistent field naming.

Splunk Detection Use Cases

1. Unauthorized IAM Role Changes or Account Modifications
This detection identifies attempts to escalate privileges or modify access pathways within internal systems.

SPL Query:
index=iam_logs action IN ("role_change","permission_change", "account_created")
| stats count BY user, action, target_user | where count > 0

Rationale: Privilege escalation is a high-impact event in a FinTech environment because it can directly enable unauthorized access to financial systems. This detection provides a low-noise, high-value signal.

2. Unusual Outbound Network Traffic Suggesting Data Exfiltration
This uses VPC flow logs to aggregate outbound traffic volume by source IP and flags systems that exceed a defined threshold.

SPL Query:
index=vpc_flow_logs direction="outbound" | stats sum(bytes) AS total_bytes BY src_ip
| where total_bytes > 300000000

Rationale: Outbound data volume is a reliable early indicator of data exfiltration, especially when correlated with identity or application activity.

3. High-Volume Failed Logins Indicating Credential Stuffing
This identifies credential stuffing, brute-force login attempts, and early signs of account takeover.

SPL Query:
index=web_logs status=401 | stats count AS failed_logins BY src_ip
| where failed_logins > 40

Rationale: Credential stuffing is a common attack vector against financial applications due to the high value of compromised accounts. This detection provides a straightforward mechanism for identifying automated login attempts.
