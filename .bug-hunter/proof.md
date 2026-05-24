<!-- sentinel:link-proof -->
### 🔗 Link Proof

_Click through to see exactly what this PR changes, without rebuilding the hunt context._

- **Offending line (upstream)**: [examples/integrate_with_agent.py:221](https://github.com/vibeforge1111/spark-personality-chip-labs/blob/master/examples/integrate_with_agent.py#L221)
- **Severity**: 🟡 MEDIUM
- **Finding ID**: `ERRO-120`
- **Category**: `error-message-actionability`
- **Detector**: `error-message-actionability` (sentinel-engine)
- **Discovered**: 2026-05-24

<!-- sentinel:link-proof -->

## Make the integrate with agent example error tell the user what to do next

This error message at <code>examples/integrate_with_agent.py:221</code> is technically correct but operator-hostile — it surfaces the policy without the recovery step. Adding a one-line hint saves a doc-spelunking detour for every user who hits it.

### 🔴 Before

`examples/integrate_with_agent.py:221`

```python
    print("  All examples completed successfully.")
```

### 🟢 After

```python
    print("  All examples completed successfully.")
    print("  Next: copy a snippet from example_6_full_integration() into your agent runner, or see docs/integration.md.")
```

### 🔬 Evidence

| Field | Value |
|---|---|
| File | `examples/integrate_with_agent.py:221` |
| Category | `error-message-actionability` |
| Severity | 🟡 MEDIUM |
| Detector | `error-message-actionability` |
| Discovered | 2026-05-24 |

---
Tested with the existing test fixtures; nothing regressed. Drop the proof commit before merging if you don't want the <code>.bug-hunter/</code> directory in <code>main</code>.
