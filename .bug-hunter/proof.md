<!-- sentinel:link-proof -->
### 🔗 Link Proof

_Click through to see exactly what this PR changes, without rebuilding the hunt context._

- **Offending line (upstream)**: [scripts/personality_cli.py:104](https://github.com/vibeforge1111/spark-personality-chip-labs/blob/master/scripts/personality_cli.py#L104)
- **Severity**: 🟡 MEDIUM
- **Finding ID**: `ERRO-923`
- **Category**: `error-message-actionability`
- **Detector**: `error-message-actionability` (sentinel-engine)
- **Discovered**: 2026-05-24

<!-- sentinel:link-proof -->

## Surface the next step alongside the personality cli script error

This error message at <code>scripts/personality_cli.py:104</code> is technically correct but operator-hostile — it surfaces the policy without the recovery step. Adding a one-line hint saves a doc-spelunking detour for every user who hits it.

### 🔴 Before

`scripts/personality_cli.py:104`

```python
        print("Active personality: None")
```

### 🟢 After

```python
        print("Active personality: None")
        print("  Run 'personality_cli.py activate <personality_id>' to activate one (e.g. 'activate artemis'). Use 'list' to see available chips.")
```

### 🔬 Evidence

| Field | Value |
|---|---|
| File | `scripts/personality_cli.py:104` |
| Category | `error-message-actionability` |
| Severity | 🟡 MEDIUM |
| Detector | `error-message-actionability` |
| Discovered | 2026-05-24 |

---
Single-purpose change. Compile-verified locally; behavior unchanged for the success path.
