# SOC Lab - Networking

## Network

The lab uses a VirtualBox Host-Only network:

```text
10.10.10.0/24
```

Current addresses:

| Host            | Role     | IP            |
| --------------- | -------- | ------------- |
| `wazuh-lab`     | SOC      | `10.10.10.10` |
| `ubuntu-server` | Target   | `10.10.10.11` |
| `kali`          | Attacker | `10.10.10.12` |
The machines also have a NAT interface for Internet access.

---
## Why Two Networks?

I use the Host-Only network for communication inside the lab.

NAT is used when a machine needs Internet access, for example to install updates or software.

This keeps the attack traffic inside the lab network instead of using my normal home network.

## Main Communication

The main traffic in the lab will be:

```text
kali
  |
  | attacks
  |
ubuntu-server
  |
  | telemetry
  |
wazuh-lab
```

The Wazuh Agent on `ubuntu-server` sends information to the Wazuh Manager on `wazuh-lab`.

## Network Validation

The following connectivity was tested:
```
kali -> ubuntu-server         [OK]
ubuntu-server -> wazuh-lab    [OK]
kali -> wazuh-lab             [OK]
Internet access through NAT   [OK]
```