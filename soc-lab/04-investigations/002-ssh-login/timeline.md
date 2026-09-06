# Investigation 002 - Timeline

| Time | Event                        | Source              | Rule | Notes |
| ---- | ---------------------------- | ------------------- | ---: | ----- |
| TBD  | Authentication failure       | Linux / Wazuh       |  TBD |       |
| TBD  | Authentication failure       | Linux / Wazuh       |  TBD |       |
| TBD  | Repeated failures detected   | Wazuh               |  TBD |       |
| TBD  | Authentication success       | Linux / Wazuh       |  TBD |       |
| TBD  | Session opened               | Linux / Wazuh       |  TBD |       |
| TBD  | Post-authentication activity | Linux Audit / Wazuh |  TBD |       |
| TBD  | Session closed               | Linux / Wazuh       |  TBD |       |

---
## Sequence

```text
Failed authentication
        ↓
Failed authentication
        ↓
Repeated failures
        ↓
Successful authentication
        ↓
Session
        ↓
Post-authentication activity
        ↓
Session closed
```

---
## Result

The timeline will be completed after the SSH experiment is performed.