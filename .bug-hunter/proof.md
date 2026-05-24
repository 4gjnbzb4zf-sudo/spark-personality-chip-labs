<!-- sentinel:link-proof -->
### 🔗 Link Proof

_Click through to see exactly what this PR changes, without rebuilding the hunt context._

- **Offending line (upstream)**: [scripts/personality_cli.py:90](https://github.com/vibeforge1111/spark-personality-chip-labs/blob/master/scripts/personality_cli.py#L90)
- **Severity**: 🟡 MEDIUM
- **Finding ID**: `ERRO-193`
- **Category**: `error-message-actionability`
- **Detector**: `error-message-actionability` (sentinel-engine)
- **Discovered**: 2026-05-24

<!-- sentinel:link-proof -->

## Surface the next step alongside the personality cli script error

The error at <code>scripts/personality_cli.py:90</code> names what went wrong but not what to do about it. An operator hitting this message has to read source to figure out the fix — which is exactly the kind of friction that turns minor failures into hour-long debug sessions.

### 🔴 Before

`scripts/personality_cli.py:90`

```python
    else:
        print("Active personality: None")

    print(f"\nActive file: {ACTIVE_FILE}")
```

### 🟢 After

```python
    else:
        print("Active personality: None")
        print("Run 'personality_cli.py activate <personality_id>' to activate one (use 'list' to see available chips).")

    print(f"\nActive file: {ACTIVE_FILE}")
```

### 🔬 Evidence

| Field | Value |
|---|---|
| File | `scripts/personality_cli.py:90` |
| Category | `error-message-actionability` |
| Severity | 🟡 MEDIUM |
| Detector | `error-message-actionability` |
| Discovered | 2026-05-24 |

---
Single-purpose change. Compile-verified locally; behavior unchanged for the success path.
