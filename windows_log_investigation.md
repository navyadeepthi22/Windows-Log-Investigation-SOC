# Windows Log Investigation for SOC Analysts

## Objective
To analyze Windows authentication logs and identify suspicious login activity using Windows Security Event logs.

## Important Windows Event IDs
- 4624 – Successful login
- 4625 – Failed login
- 4634 – Logoff
- 4672 – Special privileges assigned
- 4720 – User account created

## Case Study: Suspicious Login Activity

### Scenario
Multiple failed login attempts followed by abnormal authentication behavior were detected on a Windows system during non-business hours.

### System Context
The system was running Windows Home edition, which does not support advanced audit policy configuration. Due to this limitation, failed interactive logon attempts were recorded as session termination events (Event ID 4634) instead of Event ID 4625.

### Observed Events
- Event ID 4634: Multiple session terminations
- Event ID 4624: Successful login after abnormal activity
- Event ID 4672: Privileged access assigned

### Timeline Analysis
- Activity occurred outside business hours
- Multiple session terminations in a short time window

## Analysis
Security logs were reviewed to determine the nature of the alert. Repeated Event ID 4634 entries for the same user indicate abnormal authentication behavior that can be associated with failed login attempts or abrupt session termination.

The activity timing and user context increased suspicion, especially as the user belonged to a sensitive department. Although Event ID 4625 was not logged due to system limitations, correlation of event patterns suggested possible unauthorized or brute-force login attempts.

## MITRE ATT&CK Mapping
- Tactic: Credential Access
- Technique: Brute Force (T1110)

## Decision
True Positive – Escalated to Tier-2 SOC

## Recommended Actions
- Temporarily lock the affected user account
- Reset user credentials
- Review VPN and firewall logs
- Notify the user and IT security team

## Purpose
This project demonstrates practical Windows log investigation skills, event correlation, and SOC analyst decision-making.
