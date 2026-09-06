# Investigation 001 - File Integrity Monitoring

## Objective

Test whether Wazuh can detect a file being created, modified, and deleted on the monitored endpoint.

---
## Scenario

I created a test directory on `ubuntu-server` and configured Wazuh FIM to monitor it in real time.

The test file was:

```text
/home/ubuntu/soc-monitor/test.txt
```

I then ran:

```bash
touch ~/soc-monitor/test.txt
echo "SOC laboratory test" > ~/soc-monitor/test.txt
rm ~/soc-monitor/test.txt
```

---
## Evidence

Three Wazuh events were generated:
### 1. File created
- Rule: `554`
- File: `/home/ubuntu/soc-monitor/test.txt`
- User: `ubuntu`
- Size: `0 bytes`
- MD5: `d41d8cd98f00b204e9800998ecf8427e`

### 2. File modified
- Rule: `550`
- File: `/home/ubuntu/soc-monitor/test.txt`
- Size: `0 → 20 bytes`
- MD5 changed from `d41d8cd98f00b204e9800998ecf8427e`  
    to `426cb1f022b51050f8ba4bd4d3d3452a`

### 3. File deleted
- Rule: `553`
- File: `/home/ubuntu/soc-monitor/test.txt`
- User: `ubuntu`

---
## Timeline

The detailed timeline is available in [[soc-lab/04-investigations/001-file-integrity-monitoring/timeline|timeline.md]].

---
## Analysis

The events show that the monitored file was created as an empty file, later modified, and then deleted.

The file size and MD5 change provide evidence that its contents changed between the creation and modification events.

The events were associated with the `ubuntu` account.

## Initial Assessment

The activity itself was not suspicious because it was intentionally generated as part of this laboratory exercise.

The experiment did, however, confirm that Wazuh can detect filesystem changes in a directory configured for monitoring.

---
## Limitations

FIM showed that the file changed, but the available evidence did not identify:
- Which process performed the change
- Which command caused the change
- Why the change happened

---
## Conclusion

The test was successful. Wazuh detected the creation, modification, and deletion of the monitored file.

The experiment also showed that only configured paths are monitored.

---
## What I Learned

I learned that an active Wazuh Agent does not automatically mean every file on an endpoint is being monitored.

I also learned that a FIM alert describes a filesystem change, but more telemetry is needed to understand what caused the change.