# SOC Lab

A personal cybersecurity lab that I am building while learning SOC analysis, security monitoring, and incident investigation.

My longer-term goal is to move from SOC work into DFIR and malware analysis, so I am using this lab to build the fundamentals first.

A more detailed overview of my objectives is available in [[lab-objectives|lab-objectives.md]]

---
## Lab Architecture

The lab architecture I followed is detailed in [[architecture|architecture.md]]

---
## Project 01 - Mini SOC

**Status: In progress**

Completed so far:
- VirtualBox lab
- Isolated Host-Only network
- Wazuh installation
- Wazuh Agent deployment
- Linux Audit installation
- File Integrity Monitoring
- First FIM investigation

Currently working on:
- SSH attack simulation
- Authentication investigation
- Process and command visibility
- Detection engineering

---
## Investigations

### 001 - File Integrity Monitoring

Tested creation, modification, and deletion of a monitored file using Wazuh FIM.

### 002 - SSH Authentication

Investigating repeated SSH authentication failures followed by a successful login.

---
## Repository

```text
01-foundation/
    Lab architecture and networking

02-wazuh/
    Wazuh installation and endpoint setup

03-detections/
    Detection work

04-investigations/
    Security investigations

05-incident-response/
    Future incident-response exercises

assets/
    Screenshots and other useful images
```
---
## Templates

I will use a set of templates for each investigation and timeline to keep everything consistent.
	* More templates might be added in the future.

The template for the investigations: [[investigation-template|investigation-template.md]].

The template for the timelines: [[timeline-template|timeline-template.md]].
	* Some timelines might need more fields than the presented for a better understanding.