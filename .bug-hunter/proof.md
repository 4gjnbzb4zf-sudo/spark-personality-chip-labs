<!-- sentinel:link-proof -->
### 🔗 Link Proof

_Click through to see exactly what this PR changes, without rebuilding the hunt context._

- **Offending line (upstream)**: [src/personality_engine/room_reader.py:180](https://github.com/vibeforge1111/spark-personality-chip-labs/blob/master/src/personality_engine/room_reader.py#L180)
- **Severity**: 🟢 LOW
- **Finding ID**: `SILE-430`
- **Category**: `silent-failure`
- **Detector**: `silent-failure` (sentinel-engine)
- **Discovered**: 2026-05-24

<!-- sentinel:link-proof -->

## Log the room reader personality engine failure instead of swallowing it

This <code>except</code> block at <code>src/personality_engine/room_reader.py:180</code> drops the exception and continues. Operators investigating a failure read every log line in the path and find nothing. The clue lives only in the caller's return value, which the caller usually treats as fine.

### 🔴 Before

`src/personality_engine/room_reader.py:180`

```python
    except OSError:
        pass
```

### 🟢 After

```python
    except OSError as e:
        import logging
        logging.getLogger(__name__).warning("Failed to save room trajectory: %s", e)
```

### 🔬 Evidence

| Field | Value |
|---|---|
| File | `src/personality_engine/room_reader.py:180` |
| Category | `silent-failure` |
| Severity | 🟢 LOW |
| Detector | `silent-failure` |
| Discovered | 2026-05-24 |

---
Single-purpose change. Compile-verified locally; behavior unchanged for the success path.
