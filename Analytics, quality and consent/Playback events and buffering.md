# Playback Events and Buffering

A video player is a **state machine**. Every time its **state changes**, it **fires an event**. **Analytics tools listen** to these events and **send them to a server**.

```
Player state changes → event fired → analytics tool → server
```

## Playback Events

| Event                         | Meaning                                                    |
| ----------------------------- | ---------------------------------------------------------- |
| **load / start**              | Player has loaded the video and is ready                   |
| **play / pause**              | User or app started or paused playback                     |
| **seek**                      | User jumped to another position                            |
| **buffer start / buffer end** | Player ran out of data and is waiting, then recovered      |
| **progress**                  | Fires repeatedly with the current position                 |
| **error**                     | Playback failed                                            |
| **end**                       | Video finished                                             |

---

## What Buffering Is

The player **downloads video ahead of the playhead**. If the **network is slower than the video bitrate**, the **buffer empties** and **playback stalls** while it waits.

> That is **"buffering"**, the spinner viewers hate.

### Two Kinds of Buffering

Analytics **separates them**, because they feel very different to the viewer:

| Kind                   | When it happens                     | How bad it is                                |
| ---------------------- | ----------------------------------- | -------------------------------------------- |
| **Startup buffering**  | The wait **before the first frame** | Users **tolerate a little**                  |
| **Rebuffering**        | Stalls **mid-playback**             | **Hurts the experience much more**           |

---

## Example: A Real Stream

```
play → buffer_start → buffer_end → (playing) → buffer_start → buffer_end → (playing) → video_end
       └──── startup buffering ────┘            └──── rebuffering ─────┘
                                                  (network dip)
```

| Step | Event            | What's happening                                  |
| ---- | ---------------- | ------------------------------------------------- |
| 1    | `play`           | User presses play                                 |
| 2    | `buffer_start`   | Player waits for data before the first frame      |
| 3    | `buffer_end`     | First frame shows, playback runs                  |
| 4    | `buffer_start`   | The **network dips**, playback stalls             |
| 5    | `buffer_end`     | Playback recovers                                 |
| 6    | `video_end`      | Video finished                                    |

> From those **timestamps** you can compute **startup time** and **rebuffer time**.

| Metric            | Computed from                                                 |
| ----------------- | ------------------------------------------------------------- |
| **Startup time**  | `play` → first `buffer_end`                                   |
| **Rebuffer time** | Sum of every later `buffer_start` → `buffer_end`              |
