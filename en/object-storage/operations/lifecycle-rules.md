# Lifecycle Rules

Lifecycle rules automatically transition objects to cheaper storage or delete expired data.

### Example policies
| Action | Rule |
|---|---|
Move to Cold Storage | after 30 days
Move to Archive | after 90 days
Delete object | after 365 days

### Create rule
Console → Bucket → Lifecycle → Add rule

### Example JSON
```json
{
  "rule": {
    "prefix": "logs/",
    "transitions": [
      { "days": 30, "storageClass": "COLD" },
      { "days": 90, "storageClass": "ARCHIVE" }
    ],
    "expiration": { "days": 365 }
  }
}
```
