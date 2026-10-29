# What Google Returns

Google returns **two things**:

| What                | Description                                                                         |
| ------------------- | ----------------------------------------------------------------------------------- |
| **Stream URL**      | One URL that **already has the ads stitched** into the content. The player just plays it |
| **Ad-break times**  | A list saying **where each ad break starts and ends**, and **how long** it is      |

> **The URL gives you the video. The times give you the knowledge of where the ads are.**
>
> Without the times, the player sees **one continuous video** and **can't tell an ad from the content**.

## Example Response

A simplified response, shown as JSON to make the idea concrete:

```json
{
  "adBreaks": [
    { "type": "pre",  "start": 0,    "end": 30   },
    { "type": "mid",  "start": 1830, "end": 1845 },
    { "type": "post", "start": 5445, "end": 5460 }
  ]
}
```

| Break    | Start (s) | End (s) | Length (s) |
| -------- | --------- | ------- | ---------- |
| **Pre**  | 0         | 30      | 30         |
| **Mid**  | 1830      | 1845    | 15         |
| **Post** | 5445      | 5460    | 15         |

### The Two-Timelines Issue

Notice the **mid-roll starts at 1830, not 1800**.

The **30 seconds of pre-roll are inside the stream**, so **everything after it shifts by 30 seconds**. That is the **two-timelines issue**.

```
Content time:          0 ─────────────────── 1800 (mid-roll point)
Stream time:   [pre 30s] 30 ─────────────────── 1830 (mid-roll starts)
```

---

## Pros and Cons

### Getting the URL and Break Times Together

| ✅ Pros                                                       | ❌ Cons                                                            |
| ------------------------------------------------------------ | ----------------------------------------------------------------- |
| The **player stays simple**: one URL, no ad logic            | The app **must build and maintain the ad UI** itself              |
| The break times let the app **build any ad UI** it wants     | If the times are **wrong or arrive late**, the UI is wrong        |

### Stream URL Expiring or Being Tied to a Session

| ✅ Pros                                                             | ❌ Cons                                                                                                 |
| ------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------ |
| Google can **track the viewing session** and **report ads properly** | The URL is **not a permanent link**. You can't save it and reuse it later; you **request a new stream each time** |
