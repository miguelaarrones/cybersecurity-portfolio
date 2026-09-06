# Investigation 002 - SSH Authentication

## Objective

Investigate repeated SSH authentication failures against an account on `ubuntu-server` and determine whether the activity is suspicious.

---
## Scenario

The activity will be generated from:

```text
Source:
kali
10.10.10.12
```

against:

```text
Target:
ubuntu-server
10.10.10.11

Account:
ubuntu
```

The test will consist of several failed password attempts followed by a successful login.

---
## Evidence

The investigation will use:
- Linux authentication logs
- Wazuh alerts
- Session information
- Linux Audit events

The individual events and their timestamps will be recorded here after the test.

---
## Timeline

The detailed timeline will be available in [[soc-lab/04-investigations/002-ssh-login/timeline|timeline.md]].

---
## Analysis

The investigation will compare the authentication events with the additional telemetry collected from `ubuntu-server`.

The main goal is to determine whether the available evidence can show what happened before and after the successful login.

## Initial Assessment

Repeated authentication failures can have several explanations, including:
- Legitimate password-entry mistakes
- A misconfigured application
- An authentication attack

A successful login after repeated failures makes the activity more interesting and requires further investigation.

---
## Limitations

This section will record any information that cannot be established from the available telemetry.

Examples may include:
- Exact process responsible
- Commands executed
- Reason for the login
- Whether the activity was authorized

---
## Conclusion

This section will contain the final conclusion after the experiment has been completed and the evidence reviewed.

## What I Learned

This section will contain the main lessons from the investigation.