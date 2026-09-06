# Wazuh - Installation

## Objective

Install the central Wazuh components used by the lab.

---
## Server

```text
Hostname: wazuh-lab
OS: Ubuntu Server 24.04
IP: 10.10.10.10
Architecture: amd64
Wazuh: 4.14.7
```

## Components

The Wazuh installation uses:
- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard

All three components are installed on `wazuh-lab`.

---
## Installation

I used the official Wazuh installation assistant to perform the initial all-in-one installation.

The generated credentials are stored locally and are not included in this repository.

---
## Validation

After the installation, I verified that the three services were running:

```text
wazuh-manager      Active
wazuh-indexer      Active
wazuh-dashboard    Active
```

I was also able to access the Wazuh Dashboard from my host computer.

---
## What I Learned

The Wazuh installation gives me the central part of the SOC, but it is not useful for investigations until an endpoint is sending telemetry to it.