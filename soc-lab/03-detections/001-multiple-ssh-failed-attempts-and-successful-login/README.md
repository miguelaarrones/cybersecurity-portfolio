# Detection 001 - Multiple SSH Failed Attempts Followed by Successful Login

## Objective

I want to detect multiple SSH authentication failures followed by a successful login.
## Detection Logic

The detection looks for a sequence of SSH authentication events.

First, rule `100100` detects 5 failed SSH authentication attempts from the same source IP and against the same user within 30 seconds.

Then, rule `100101` looks for a successful SSH authentication from the same source IP and for the same user after rule `100100` has triggered.

The idea is to identify a pattern that could indicate password guessing or the use of guessed or stolen credentials.
## Telemetry

For this detection I think we need:
- Source IP
- Target IP
- Target user
- Authentication result
- Timestamps
- Number of failed attempts
## Threshold

### Lab threshold

5 failed attempts within 30 seconds, followed by a successful login.

This makes the behavior easy to reproduce consistently in the lab.

### Real-world starting hypothesis

10 failed attempts within 10 seconds, followed by a successful login.

I chose this as an initial hypothesis because a high number of failures in a very short period is less likely to be caused by a normal user manually entering a password and may indicate automated password guessing.

This threshold would need to be tested and adjusted depending on the environment.
## Rules

```xml
<rule id="100100" level="10" frequency="5" timeframe="30">
    <if_matched_sid>5760</if_matched_sid>
    <same_srcip />
    <same_user />
    <description>SSH: 5 authentication failures from the same source and user within 30 seconds.</description>
    <group>authentication_failed,ssh,custom_detection,</group>
</rule>

<rule id="100101" level="12" timeframe="30">
    <if_sid>5715</if_sid>
    <if_matched_sid>100100</if_matched_sid>
    <same_srcip />
    <same_user />
    <description>SSH: Multiple authentication failures followed by successful login.</description>
    <group>authentication_success,authentication_failed,ssh,custom_detection,</group>
    <mitre>
        <id>T1110</id>
    </mitre>
</rule>
```
## Testing

I performed two tests using Wazuh's tool `/var/ossec/bin/wazuh-logtest`.

The first test consisted of 5 failed authentication attempts followed by a successful authentication attempt. This resulted in Wazuh triggering rule `100100`, followed by rule `100101`.

The second test consisted of 4 failed authentication attempts followed by a successful authentication attempt. This did not trigger either of the custom rules.

The positive test confirmed that the detection triggers when the defined threshold is reached, while the negative test confirmed that the detection does not trigger below the threshold.
## Results

The detection can identify a sequence of multiple failed SSH authentication attempts followed by a successful login.

This pattern could potentially indicate malicious activity, such as password guessing, but it should be investigated together with other available evidence.
## False Positives

A user entering the wrong password several times, or a service using an outdated or incorrect password, could generate the same pattern.

A threshold is therefore needed to reduce unnecessary alerts.
## What I Learned

I learned how to identify what Wazuh is already detecting, create custom rules based on a specific behavior, and test the detection with both positive and negative cases.

I also learned that a useful detection does not always need to detect a completely new event. It can correlate events that Wazuh is already detecting separately.