# Investigation 003 - Timeline

| Time     | Event                             | Source      | Rule | Notes                                                    |
| -------- | --------------------------------- | ----------- | ---: | -------------------------------------------------------- |
| 17:51:56 | whoami                            | Linux Audit |  --- | Session `22`, PPID `3592`, `uid: ubuntu`, `auid: ubuntu` |
| 17:51:57 | id                                | Linux Audit |  --- | Session `22`, PPID `3592`, `uid: ubuntu`, `auid: ubuntu` |
| 17:52:00 | sudo -i                           | Linux Audit |  --- | Session `22`, PPID `3592`, `uid: ubuntu`, `auid: ubuntu` |
| 17:52:02 | Root shell created                | Linux Audit |  --- | Session `22`, PPID `3592`, `uid: root`, `auid: ubuntu`   |
| 17:52:04 | whoami                            | Linux Audit |  --- | Session `22`, PPID `3592`, `uid: root`, `auid: ubuntu`   |
| 17:52:04 | id                                | Linux Audit |  --- | Session `22`, PPID `3592`, `uid: root`, `auid: ubuntu`   |
| 17:52:05 | Successful sudo to ROOT executed. | Wazuh       | 5402 |                                                          |
| 17:52:12 | cat /etc/shadow                   | Linux Audit |  --- | Session `22`, PPID `3592`, `uid: root`, `auid: ubuntu`   |
| 17:52:33 | Failed sudo to root               | Wazuh       | 5401 |                                                          |

---
## Sequence

```text
17:51:56
whoami executed by ubuntu user
        ↓
17:51:57
id executed by ubuntu user
        ↓
17:52:00
Privilege escalation attempt performed by ubuntu user
        ↓
17:52:02
Root shell created
        ↓
17:52:04
whoami executed by root
        ↓
17:52:04
id executed by root
        ↓
17:52:05
Wazuh reports a successful sudo to ROOT
        ↓
17:52:12
cat /etc/shadow executed by root
        ↓
17:52:33
Wazuh reports a failed sudo to ROOT
```