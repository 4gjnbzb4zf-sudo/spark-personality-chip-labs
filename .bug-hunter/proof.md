<!-- sentinel:link-proof -->
### 🔗 Link Proof

_Click through to see exactly what this PR changes, without rebuilding the hunt context._

- **Offending line (upstream)**: [src/personality_engine/hooks.py:132](https://github.com/vibeforge1111/spark-personality-chip-labs/blob/master/src/personality_engine/hooks.py#L132)
- **Severity**: 🟢 LOW
- **Finding ID**: `SILE-917`
- **Category**: `silent-failure`
- **Detector**: `silent-failure` (sentinel-engine)
- **Discovered**: 2026-05-24

<!-- sentinel:link-proof -->

## Log the hooks personality engine failure instead of swallowing it

The exception handler at <code>src/personality_engine/hooks.py:132</code> catches the error and returns a failure-shaped result without logging. If this fires in production, you'll never see it in the application's own logs — only the downstream consumer notices, usually as silent data loss.

### 🔴 Before

`src/personality_engine/hooks.py:132`

```python
    try:
        write_bridge(chip, session_id=session_id)
    except Exception:
        pass  # Bridge write failure shouldn't block context injection
```

### 🟢 After

```python
    try:
        write_bridge(chip, session_id=session_id)
    except Exception as e:
        import logging
        logging.getLogger(__name__).warning("Bridge write failed: %s", e)
        # Bridge write failure shouldn't block context injection
```

### 🔬 Evidence

| Field | Value |
|---|---|
| File | `src/personality_engine/hooks.py:132` |
| Category | `silent-failure` |
| Severity | 🟢 LOW |
| Detector | `silent-failure` |
| Discovered | 2026-05-24 |

---
Single-purpose change. Compile-verified locally; behavior unchanged for the success path.
