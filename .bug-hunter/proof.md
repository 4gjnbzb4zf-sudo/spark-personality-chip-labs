<!-- sentinel:link-proof -->
### 🔗 Link Proof

_Click through to see exactly what this PR changes, without rebuilding the hunt context._

- **Offending line (upstream)**: [src/personality_engine/hooks.py:66](https://github.com/vibeforge1111/spark-personality-chip-labs/blob/master/src/personality_engine/hooks.py#L66)
- **Severity**: 🟢 LOW
- **Finding ID**: `SILE-469`
- **Category**: `silent-failure`
- **Detector**: `silent-failure` (sentinel-engine)
- **Discovered**: 2026-05-24

<!-- sentinel:link-proof -->

## Surface the swallowed exception in hooks personality engine so operators can trace it

This <code>except</code> block at <code>src/personality_engine/hooks.py:66</code> drops the exception and continues. Operators investigating a failure read every log line in the path and find nothing. The clue lives only in the caller's return value, which the caller usually treats as fine.

### 🔴 Before

`src/personality_engine/hooks.py:66`

```python
    except (json.JSONDecodeError, OSError):
        pass
    return {}
```

### 🟢 After

```python
    except (json.JSONDecodeError, OSError) as exc:
        sys.stderr.write(f"personality_engine: failed to read hook stdin: {exc}\n")
    return {}
```

### 🔬 Evidence

| Field | Value |
|---|---|
| File | `src/personality_engine/hooks.py:66` |
| Category | `silent-failure` |
| Severity | 🟢 LOW |
| Detector | `silent-failure` |
| Discovered | 2026-05-24 |

---
Tested with the existing test fixtures; nothing regressed. Drop the proof commit before merging if you don't want the <code>.bug-hunter/</code> directory in <code>main</code>.
