# Resume from Continue Watching

When a viewer opens a title from **Continue Watching**, the app starts playback at a **saved position**, for example **minute 45** of the movie.

To the player, jumping straight to minute 45 **looks exactly like a seek** that skips over ad breaks: the **pre-roll** and the **mid-rolls before minute 45**.

```
[pre-roll] ── content ── [mid-roll] ── content ── ● minute 45 (saved position)
     ▲                        ▲
     └─ breaks "skipped" by jumping straight to minute 45
```

## The Bug

If you treat it as a **normal seek**, **snapback fires**. The viewer taps **"Resume"** and gets an ad from a break they **already watched yesterday**.

> **Resume should be a starting position, not a user seek.**

| Action                    | Treated as             | Snapback?   |
| ------------------------- | ---------------------- | ----------- |
| **User seek**             | A seek past ad breaks  | ✅ Yes      |
| **Resume (correct)**      | A starting position    | ❌ No       |
| **Resume (bug)**          | A normal seek          | ⚠️ Yes, the viewer sees an old ad again |

---

## Common Mistakes

| Mistake                                         | What goes wrong                                                                 |
| ----------------------------------------------- | ------------------------------------------------------------------------------- |
| **Calling the same `onSeek` handler for resume** | Snapback fires                                                                 |
| **Saving stream time as the resume position**   | The next session starts in the wrong place, because the **ads can differ each time** |
| **Reusing the old stream URL**                  | You should **request a new one** instead                                        |
| **Seeking before the stream has loaded**        | The seek is **ignored** or **lands at 0**                                       |
