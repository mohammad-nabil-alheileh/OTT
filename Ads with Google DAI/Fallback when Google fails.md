# Fallback When Google Fails

When **Google itself fails** (the stream request errors out, times out, or returns no usable stream), the app **plays a backup stream without ads** instead of showing an error screen.

```
Stream request to Google DAI
   ├── OK ─────────▶ play DAI stream (with ads)
   └── failed ─────▶ play backup stream (no ads)
```

## What Counts as "Google Failed"

| # | Failure                                           |
| - | ------------------------------------------------- |
| 1 | The stream request **returns an error or times out** |
| 2 | The response has **no stream URL**                |
| 3 | The stream URL is returned but **fails to play**  |

## The Ad UI Switches Off by Itself

With no ads, there is **only one timeline**, so these all **switch off by themselves**:

| Ad feature            | With DAI stream | With backup stream |
| --------------------- | --------------- | ------------------ |
| **Seekbar markers**   | ✅ Shown        | ❌ None            |
| **Skip button**       | ✅ Shown        | ❌ None            |
| **Snapback logic**    | ✅ Active       | ❌ Off             |
| **Timelines**         | Two             | One                |

> The UI keeps working with an **empty list of ad breaks**, with **no special case**.

## Where the Backup URL Comes From

Usually the **same content metadata or remote config**, so it can be **changed without a release**.

---

## Why It Matters

| Topic                               | Detail                                                                                                         |
| ----------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| **Log every fallback**              | If Google fails silently for a week, you only notice when **ad revenue drops**                                 |
| **Tune the timeout**                | **Too short** means ads are lost on slow networks. **Too long** means a long black screen at startup          |
| **Switching mid-playback is harder** | If DAI fails halfway, resume the backup at the **content time**, not the stream time                          |
