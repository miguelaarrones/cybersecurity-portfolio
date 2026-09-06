# Wazuh - Agent Deployment

## Objective

Install and configure the Wazuh Agent on `ubuntu-server`.

---
## Target

```text
Hostname: ubuntu-server
OS: Ubuntu Server 24.04
IP: 10.10.10.11
Role: Monitored endpoint
```

---
## Agent

The Wazuh Agent is installed on `ubuntu-server` and sends endpoint information to the Wazuh Manager running on `wazuh-lab`.

The target is currently the only monitored endpoint in the lab.

## Telemetry

The first telemetry sources I am interested in are:
- SSH authentication
- File changes
- Linux Audit events
- Process execution

---
## Linux Audit

I installed `auditd` on `ubuntu-server`.

The Wazuh Agent is configured to collect:

```text
/var/log/audit/audit.log
```

The purpose of this is to get more information about process and command execution during investigations.

---
## Validation

The setup was tested by checking:

```text
Agent installed              [OK]
Agent running                [OK]
Agent enrolled               [OK]
Agent visible in Dashboard   [OK]
Agent status Active          [OK]
Target can reach Wazuh       [OK]
```

---
## What I Learned

Installing an agent is only the beginning. The important part is deciding what information should be collected so that an investigation can actually be performed.