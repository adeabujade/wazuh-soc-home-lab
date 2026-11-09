# Wazuh SIEM SOC Home Lab

## Project Overview

Built a hands-on Security Operations Center (SOC) home lab using Wazuh SIEM to monitor Windows endpoint activity, collect security events, and investigate authentication failures.

Deployed Wazuh on an Ubuntu virtual machine and connected a Windows endpoint using the Wazuh Agent. Successfully enrolled the endpoint, verified communication, and investigated Windows Security Event ID 4625.

## Tools & Technologies

- Wazuh SIEM 4.14.10
- Ubuntu Linux
- Windows Endpoint
- Oracle VirtualBox
- Windows Security Event Logs
- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard
- TCP/IP Networking

## Lab Architecture

- Ubuntu VM hosting the Wazuh SIEM components.
- Windows computer running the Wazuh Agent.
- Host-only networking between the endpoint and SIEM server.
- Wazuh Dashboard for monitoring and event investigation.

## Project Implementation

### 1. Wazuh SIEM Installation

- Installed Ubuntu Linux in VirtualBox.
- Installed Wazuh Manager, Wazuh Indexer, and Wazuh Dashboard.
- Troubleshot service configuration and certificate issues.
- Configured network connectivity for endpoint communication.

### 2. Windows Agent Deployment

- Installed Wazuh Agent 4.14.10 on Windows.
- Configured the agent to communicate with the Wazuh server.
- Enrolled the endpoint using `agent-auth.exe`.
- Successfully received an enrollment key.
- Verified the endpoint appeared as active in the Wazuh Dashboard.

### 3. Security Event Generation

Generated a controlled failed authentication attempt on the Windows endpoint.

Identified and investigated:

**Windows Security Event ID 4625 — An account failed to log on.**

Used Wazuh Threat Hunting to locate and examine the event.

Search query:

```text
data.win.system.eventID:4625
```

### 4. SOC Investigation: Failed Logon

Analyzed the following event fields:

| Field | Observed Value |
|---|---|
| Event ID | 4625 |
| Source IP | 127.0.0.1 |
| Logon Type | 2 - Interactive |
| Authentication Package | Negotiate |
| Logon Process | User32 |
| Status | 0xC000006D |
| SubStatus | 0xC0000380 |
| SID | S-1-0-0 |

### Investigation Findings

- Identified a failed interactive authentication attempt.
- Determined that the source IP was the local loopback address.
- Analyzed the Windows authentication package.
- Examined the authentication failure status and substatus.
- Identified a smart-card-related PIN failure status.
- Documented findings and assessed the event.

**Initial Assessment:** The event was generated during a controlled lab exercise. The smart-card-related substatus requires further verification before attributing the failure to an ordinary incorrect-password attempt.

## Skills Demonstrated

- SIEM deployment and configuration
- Wazuh agent installation and enrollment
- Windows endpoint monitoring
- Linux system administration
- Windows Security Event Log analysis
- Authentication failure investigation
- Network troubleshooting
- Security event investigation
- Incident documentation and triage

## Project Results

Successfully deployed a Wazuh SIEM environment, connected a Windows endpoint, collected security events, and completed an initial failed-login investigation.

This project provided practical experience with endpoint monitoring, security event analysis, and SOC investigation workflows.

## Future Improvements

- Investigate repeated failed login attempts.
- Build brute-force detection rules.
- Monitor successful and failed authentication events.
- Investigate suspicious process creation.
- Create custom Wazuh detection rules.
- Document additional security incidents.
