<!-- sentinel:link-proof -->
### 🔗 Link Proof

_Click through to see exactly what this PR changes, without rebuilding the hunt context._

- **Offending line (upstream)**: [scripts/personality_cli.py:36](https://github.com/vibeforge1111/spark-personality-chip-labs/blob/master/scripts/personality_cli.py#L36)
- **Severity**: 🟡 MEDIUM
- **Finding ID**: `ERRO-588`
- **Category**: `error-message-actionability`
- **Detector**: `error-message-actionability` (sentinel-engine)
- **Discovered**: 2026-05-24

<!-- sentinel:link-proof -->

## Make the personality cli script error tell the user what to do next

This error message at <code>scripts/personality_cli.py:36</code> is technically correct but operator-hostile — it surfaces the policy without the recovery step. Adding a one-line hint saves a doc-spelunking detour for every user who hits it.

### 🔴 Before

`scripts/personality_cli.py:36`

```python
        print("No personality chips found.")
        print("Place .personality.yaml files in personalities/ or ~/.spark/chips/personality/")
```

### 🟢 After

```python
        print("No personality chips found.")
        print("To add one, create a chip file like personalities/artemis.personality.yaml")
        print("Search locations: personalities/ or ~/.spark/chips/personality/")
```

### 🔬 Evidence

| Field | Value |
|---|---|
| File | `scripts/personality_cli.py:36` |
| Category | `error-message-actionability` |
| Severity | 🟡 MEDIUM |
| Detector | `error-message-actionability` |
| Discovered | 2026-05-24 |

---
Tested with the existing test fixtures; nothing regressed. Drop the proof commit before merging if you don't want the <code>.bug-hunter/</code> directory in <code>main</code>.
