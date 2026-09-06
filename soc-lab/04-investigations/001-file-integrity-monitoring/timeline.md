# Investigation 001 - Timeline

|Time|Event|Rule|Evidence|
|---|---|--:|---|
|11:08:15.084|File created|554|`test.txt`, 0 bytes|
|11:08:18.769|File modified|550|Size changed 0 → 20 bytes, MD5 changed|
|11:08:21.826|File deleted|553|File removed|

---
## Sequence

```text
11:08:15.084
CREATE
    ↓
11:08:18.769
MODIFY
    ↓
11:08:21.826
DELETE
```

## User

```text
ubuntu
```

## File

```text
/home/ubuntu/soc-monitor/test.txt
```