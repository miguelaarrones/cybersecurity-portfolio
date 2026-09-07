# Investigation 002 - SSH Authentication

## Objective

Determine whether Wazuh can detect repeated SSH authentication attempts, consisting of four failed attempts followed by a successful login, and investigate which commands were executed during the resulting session.

---
## Scenario

I used Kali (`10.10.10.12`) to connect to `ubuntu-server` (`10.10.10.11`) using SSH. I entered an incorrect password four times and the correct password on the fifth attempt. After logging in, I ran `whoami`, `id`, and `ls`.

---
## Evidence

Wazuh generated five authentication events during the test:
- Four `sshd: authentication failed` events
- One `sshd: authentication success` event

All five events contained:
- Source IP: `10.10.10.12`
- Target IP: `10.10.10.11`
- Account: `ubuntu`

The Wazuh alerts I reviewed did not provide enough information to identify the commands executed after the successful login, so I continued the investigation directly on `ubuntu-server` using `ausearch`.

The Audit logs showed:
- Audit session: `59`
- Three commands executed: `whoami`, `id`, and `ls`
- The three command events had the same `ses` value (`59`)
- The three command events had the same parent PID (`8674`)

I then followed the PID and PPID relationships and found that:
- `PID 8674` was the `-bash` shell
- `PPID 8674` was `8673`
- The `USER_LOGIN` event was associated with `PID 8673`
- The `USER_LOGIN` event contained `addr=10.10.10.12`, matching the source IP shown by Wazuh

This allowed the command execution events to be correlated with the SSH login from `kali-attacker`.

---
## Timeline

The detailed timeline will be available in [[soc-lab/04-investigations/002-ssh-login/timeline|timeline.md]].

---
## Analysis

The timeline shows four SSH authentication attempts from `10.10.10.12` against the `ubuntu` account on `ubuntu-server`. The first four attempts failed and the fifth attempt was successful.

After the successful authentication, the commands `whoami`, `id`, and `ls` were executed while the session was open.

By following the PID/PPID relationships and matching the `addr` value from the `USER_LOGIN` event with the source IP reported by Wazuh, I was able to correlate these commands with the SSH session.

## Initial Assessment

Multiple authentication failures can have several explanations and are not necessarily malicious.

In this investigation, there were only four failed attempts before the login succeeded, so the activity could reasonably be explained by incorrect password entries.

The commands executed after the login (`whoami`, `id`, and `ls`) also do not show any obvious malicious behavior.

Based on the available evidence, I would consider the activity worth documenting and reviewing, but there is not enough evidence to classify it as malicious.

---
## Limitations

The commands executed during the SSH session were not visible in the Wazuh alerts I reviewed. I therefore had to continue the investigation directly on `ubuntu-server` using Linux Audit and `ausearch`.

Apart from this, I did not identify any other important limitations in the evidence collected for this investigation.

---
## Conclusion

The activity is consistent with a legitimate password-entry mistake. Four authentication attempts failed before the correct password was entered, and the commands executed after the login did not show any obvious malicious behavior.

Based on the evidence collected during this investigation, I would not classify the activity as malicious.

## What I Learned

- I learned how to read and understand SSH-related events in Wazuh.
- I learned that Wazuh cannot show behavior that is not covered by its current monitoring configuration.
- I learned that Wazuh is not the only source of evidence and that I can investigate the target directly when I need more information.
- I learned how to identify sessions, PIDs, and PPIDs in Linux Audit logs and use them to correlate processes with an SSH session.