<!-- sentinel:link-proof -->
### 🔗 Link Proof

_Click through to see exactly what this PR changes, without rebuilding the hunt context._

- **Offending line (upstream)**: [scripts/personality_cli.py:84](https://github.com/vibeforge1111/spark-personality-chip-labs/blob/master/scripts/personality_cli.py#L84)
- **Severity**: 🟡 MEDIUM
- **Finding ID**: `ERRO-622`
- **Category**: `error-message-actionability`
- **Detector**: `error-message-actionability` (sentinel-engine)
- **Discovered**: 2026-05-24

<!-- sentinel:link-proof -->

## Give the personality cli script error message a recovery hint

This error message at <code>scripts/personality_cli.py:84</code> is technically correct but operator-hostile — it surfaces the policy without the recovery step. Adding a one-line hint saves a doc-spelunking detour for every user who hits it.

### 🔴 Before

`scripts/personality_cli.py:84`

```python
        print("No personality was active.")
```

### 🟢 After

```python
        print("No personality was active. Run 'personality_cli.py activate <id>' to activate one (e.g. 'personality_cli.py activate artemis'), or 'personality_cli.py list' to see available chips.")
```

### 🔬 Evidence

| Field | Value |
|---|---|
| File | `scripts/personality_cli.py:84` |
| Category | `error-message-actionability` |
| Severity | 🟡 MEDIUM |
| Detector | `error-message-actionability` |
| Discovered | 2026-05-24 |

---
Tested with the existing test fixtures; nothing regressed. Drop the proof commit before merging if you don't want the <code>.bug-hunter/</code> directory in <code>main</code>.
