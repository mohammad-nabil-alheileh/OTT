# Two Timelines

With **SSAI**, the stream is the **content plus the ads, glued together**. So there are **two different clocks**:

| Clock            | What it is                                                         | Who uses it                                    | Ads count? |
| ---------------- | ------------------------------------------------------------------ | ---------------------------------------------- | ---------- |
| **Stream time**  | The position in the **stitched stream**                            | What the **player reports**                    | ✅ Yes     |
| **Content time** | The position in the **actual movie**, as if there were no ads     | What the **viewer** thinks of as "minute 5 of the movie" | ❌ No |

## Example

A movie with a **30s pre-roll** and a **15s mid-roll** at content time **30:00**:

```
Content time:            0:00 ─────────── 30:00             30:00 ─────────── 90:00
Stream time:   [pre 30s] 0:30 ─────────── 30:30 [mid 15s]   30:45 ─────────── 90:45
```

| Moment                             | Content time        | Stream time |
| ---------------------------------- | ------------------- | ----------- |
| **Pre-roll starts**                | n/a (not content)   | 0:00        |
| **Movie begins**                   | 0:00                | 0:30        |
| **Mid-roll starts**                | 30:00               | 30:30       |
| **Movie continues after mid-roll** | 30:00               | 30:45       |
| **Movie ends**                     | 90:00               | 90:45       |

> **Stream time = content time + the length of all ad breaks played so far.**
