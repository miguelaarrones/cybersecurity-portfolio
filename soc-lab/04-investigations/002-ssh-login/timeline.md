# Investigation 002 - Timeline

| Time     | Event                      | Source      | Rule | Notes                          |
| -------- | -------------------------- | ----------- | ---: | ------------------------------ |
| 19:21:10 | Authentication failure     | Wazuh       | 5760 | From `10.10.10.12` to `ubuntu` |
| 19:21:10 | Authentication failure     | Wazuh       | 5760 | From `10.10.10.12` to `ubuntu` |
| 19:21:14 | Authentication failure     | Wazuh       | 5760 | From `10.10.10.12` to `ubuntu` |
| 19:21:14 | Authentication failure     | Wazuh       | 5760 | From `10.10.10.12` to `ubuntu` |
| 19:21:19 | Authentication Success     | Wazuh       | 5715 | From `10.10.10.12` to `ubuntu` |
| 19:21:19 | User Login                 | Linux Audit |      | PID `8673`, `addr=10.10.10.12` |
| 19:21:19 | Bash Shell Started         | Linux Audit |      | PID `8674`, PPID `8673`        |
| 19:21:21 | `whoami` executed          | Linux Audit |  --- | Session `59`, PPID `8674`      |
| 19:21:22 | `id` executed              | Linux Audit |  --- | Session `59`, PPID `8674`      |
| 19:21:23 | `ls` executed              | Linux Audit |  --- | Session `59`, PPID `8674`      |
| 19:21:26 | PAM: Login session closed. | Wazuh       | 5502 | Session ended                  |

---
## Sequence

```text
19:21:10
Failed authentication
        ↓
19:21:10
Failed authentication
        ↓
19:21:14
Failed authentication
        ↓
19:21:14
Failed authentication
        ↓
19:21:19
Successful authentication
        ↓
19:21:19
USER_LOGIN
        ↓
19:21:19
-bash started
        ↓
19:21:21
whoami
        ↓
19:21:22
id
        ↓
19:21:23
ls
        ↓
19:21:26
Session Closed
```