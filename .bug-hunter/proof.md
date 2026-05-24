<!-- sentinel:link-proof -->
### 🔗 Link Proof

_Click through to see exactly what this PR changes, without rebuilding the hunt context._

- **Offending line (upstream)**: [scripts/personality_cli.py:144](https://github.com/vibeforge1111/spark-personality-chip-labs/blob/master/scripts/personality_cli.py#L144)
- **Severity**: 🟡 MEDIUM
- **Finding ID**: `ERRO-355`
- **Category**: `error-message-actionability`
- **Detector**: `error-message-actionability` (sentinel-engine)
- **Discovered**: 2026-05-24

<!-- sentinel:link-proof -->

## Surface the next step alongside the personality cli script error

This error message at <code>scripts/personality_cli.py:144</code> is technically correct but operator-hostile — it surfaces the policy without the recovery step. Adding a one-line hint saves a doc-spelunking detour for every user who hits it.

### 🔴 Before

`scripts/personality_cli.py:144`

```python
            print("Usage: personality_cli.py activate <personality_id>")
            sys.exit(1)
```

### 🟢 After

```python
            print("Usage: personality_cli.py activate <personality_id>")
            print("Run 'personality_cli.py list' to see available personality IDs, e.g. 'personality_cli.py activate artemis'.")
            sys.exit(1)
```

### 🔬 Evidence

| Field | Value |
|---|---|
| File | `scripts/personality_cli.py:144` |
| Category | `error-message-actionability` |
| Severity | 🟡 MEDIUM |
| Detector | `error-message-actionability` |
| Discovered | 2026-05-24 |

---
Tested with the existing test fixtures; nothing regressed. Drop the proof commit before merging if you don't want the <code>.bug-hunter/</code> directory in <code>main</code>.
