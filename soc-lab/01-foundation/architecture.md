# SOC Lab - Architecture

## Overview

I am using VirtualBox to keep the lab separated from my normal network and to make it easy to create different test environments.

The lab currently has three machines:
![[architecture_overview.png]]
## Machines

### `wazuh-lab`

This is the SOC machine.

It runs:
- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard

Its job is to receive and show security information from the monitored endpoint.

### `ubuntu-server`

This is the monitored target.

It runs:
- Wazuh Agent
- auditd

This is the machine that will receive the attacks and generate the telemetry that I investigate.

### `kali`

This is used to generate controlled attack activity against `ubuntu-server`.

The purpose is to create activity that can be detected and investigated from the SOC.

---
## Network

The detailed networking architecture is available in [[networking|networking.md]].

---
## Security

The attacker and target are kept inside the laboratory network so that attack simulations are not performed directly against my normal home network.

This is especially important for future exercises involving suspicious files or malware.

---
## Current Status

| Machine         |Role|Status|
|---|---|---|
| `wazuh-lab`     |SOC|Active|
| `ubuntu-server` |Monitored target|Active|
| `kali`          |Attacker|Active|
## Future Changes

The lab will be expanded when a new component is useful for the next learning objective.

Possible future additions include a Windows endpoint, more telemetry, and dedicated DFIR or malware-analysis environments.