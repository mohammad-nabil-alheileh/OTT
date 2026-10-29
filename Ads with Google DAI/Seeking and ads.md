# Seeking and Ads

When the viewer **seeks forward** in a stream with ads, they may **jump over one or more ad breaks**. Google wants those ads to **still be seen**, so the player does **snapback**.

## How Snapback Works

1. The viewer **seeks past a mid-roll**.
2. The player **snaps back** to the start of the skipped ad break.
3. The **ad plays**.
4. Then the content **continues at the position the viewer originally asked for**.

## Example

The movie has mid-rolls at content time **30:00** and **60:00**. The viewer is at **10:00** and seeks to **70:00**:

```
Viewer at 10:00 ──seek──► wants 70:00
                           │ skipped breaks: 30:00 and 60:00
                           ▼
         snapback: play the 60:00 ad first  →  then land at 70:00
```

| Step | What happens                                 | Content time |
| ---- | -------------------------------------------- | ------------ |
| 1    | Viewer is watching                           | 10:00        |
| 2    | Viewer seeks forward                         | → 70:00      |
| 3    | Player sees skipped breaks at 30:00 and 60:00 | —           |
| 4    | Player **snaps back** and plays the **60:00 ad** | 60:00    |
| 5    | Content continues where the viewer asked     | 70:00        |

> In this example, only the **60:00 ad** (the last skipped break) is played, not the one at 30:00.

---

## Seeking to 0 and the Pre-Roll

If the viewer **seeks to the start**, the **stream position 0 is the pre-roll**, not the movie.

| Seek target       | Where they expect to land     | Where they actually land        |
| ----------------- | ----------------------------- | ------------------------------- |
| **Stream time 0** | First frame of the movie      | **The pre-roll**, so they see an ad again |
