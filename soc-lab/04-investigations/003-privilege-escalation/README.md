# Investigation 003 - Privilege Escalation

## Objective

Identify when a normal user obtains elevated privileges and establish what was executed with those privileges.
## Scenario

I used Kali (`10.10.10.12`) to connect to `ubuntu-server` (`10.10.10.11`) using SSH. 

I first executed two commands to establish the normal user context. Then I performed a successful privilege escalation using `sudo -i`, verified that I had root privileges, and executed a privileged command.

I also performed a second privilege escalation attempt that failed so I could compare the successful and failed cases.
## Evidence

Wazuh generated two events related to the privilege escalation activity:
- Rule `5402` — `Successful sudo to ROOT executed.`
- Rule `5401` — `Failed attempt to run sudo.`

The Wazuh events showed that sudo activity occurred, but they did not provide enough detail to reconstruct the commands executed before and after the privilege change.

I therefore checked Linux Audit on `ubuntu-server`.

The Audit records showed the initial commands being executed as the `ubuntu` user, followed by `sudo -i` and the creation of a root shell.

The root shell then executed:
- `whoami`
- `id`
- `cat /etc/shadow`

The Audit records also showed that the original authenticated user remained `ubuntu` through the `auid` field, while the `uid` and `euid` changed to `root`.
## Timeline

The detailed timeline will be available in [[soc-lab/04-investigations/003-privilege-escalation/timeline|timeline.md]].
## Analysis

The timeline shows a successful privilege escalation performed by the `ubuntu` user using `sudo -i.

The Linux Audit records show that the activity remained associated with the same session (`ses=22`) and original authenticated user (`auid=ubuntu`).

Before the escalation, the commands were executed with `uid=ubuntu` and `euid=ubuntu`.

After `sudo -i`, a root shell was created. The following commands were then executed with `uid=root` and `euid=root`, while `auid` remained `ubuntu`.

The root shell executed `whoami`, `id`, and `cat /etc/shadow`.

Later, another `sudo -i` attempt was made and Wazuh generated Rule `5401`, indicating a failed sudo attempt.
## Initial Assessment

The evidence confirms that the `ubuntu` user successfully obtained root privileges and accessed `/etc/shadow`.

The commands executed after the privilege escalation could be legitimate administrative activity, but they could also be part of reconnaissance or further activity after gaining elevated privileges.

Based on this investigation alone, I cannot determine whether the activity was malicious.
## Limitations

Wazuh showed the privilege-escalation events but did not provide enough command-level detail to reconstruct the full activity.

Linux Audit provided the additional process and user-context information needed to understand what happened.

The available evidence also does not establish the intent behind the activity.
## Conclusion

The investigation confirmed a successful privilege escalation from the `ubuntu` account to root using `sudo -i`.

After obtaining root privileges, the user executed `whoami`, `id`, and `cat /etc/shadow`.

A later sudo attempt failed.

The activity is security-relevant, but the available evidence is not sufficient to determine whether it was malicious.
## What I Learned

I learned how to identify privilege escalation through `sudo` and how Linux Audit can show the change from a normal user to root.

I also learned that `auid`, `uid`, and `euid` can be useful for understanding who started an activity and which identity actually executed it.