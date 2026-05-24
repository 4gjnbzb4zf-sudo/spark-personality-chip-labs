<!-- sentinel:link-proof -->
### 🔗 Link Proof

_Click through to see exactly what this PR changes, without rebuilding the hunt context._

- **Offending line (upstream)**: [src/personality_engine/hooks.py:146](https://github.com/vibeforge1111/spark-personality-chip-labs/blob/master/src/personality_engine/hooks.py#L146)
- **Severity**: 🟢 LOW
- **Finding ID**: `SILE-641`
- **Category**: `silent-failure`
- **Detector**: `silent-failure` (sentinel-engine)
- **Discovered**: 2026-05-24

<!-- sentinel:link-proof -->

## Log the hooks personality engine failure instead of swallowing it

The exception handler at <code>src/personality_engine/hooks.py:146</code> catches the error and returns a failure-shaped result without logging. If this fires in production, you'll never see it in the application's own logs — only the downstream consumer notices, usually as silent data loss.

### 🔴 Before

`src/personality_engine/hooks.py:146`

```python
    # Reset emotional state for fresh session
    try:
        from .emotional_state import reset_emotional_state
        reset_emotional_state()
    except Exception:
        pass
```

### 🟢 After

```python
    # Reset emotional state for fresh session
    try:
        from .emotional_state import reset_emotional_state
        reset_emotional_state()
    except Exception as exc:
        import logging
        logging.getLogger(__name__).debug("emotional state reset failed: %s", exc)
```

### 🔬 Evidence

| Field | Value |
|---|---|
| File | `src/personality_engine/hooks.py:146` |
| Category | `silent-failure` |
| Severity | 🟢 LOW |
| Detector | `silent-failure` |
| Discovered | 2026-05-24 |

---
Single-purpose change. Compile-verified locally; behavior unchanged for the success path.
