# Subtitles, Playback States, Seeking

These are the **three things a viewer actually touches**:

| Part | Topic               | What the viewer does              |
| ---- | ------------------- | --------------------------------- |
| A    | **Subtitles**       | Reads text on screen              |
| B    | **Playback states** | Presses play or pause             |
| C    | **Seeking**         | Jumps around the timeline         |

---

## Part A: Subtitles

**Subtitles** are **text cues**, shown over the video. Each cue has:

- a **start time**
- an **end time**
- some **text**

The most common format in HLS is **WebVTT**.

### How Subtitles Fit Into HLS

1. The **master playlist** declares subtitle tracks, next to the video renditions.
2. Each subtitle track has its **own small playlist**, which points to `.vtt` segments.

> Subtitles are **chunked and downloaded just like video**.

### Two Kinds of Subtitles

| Kind                    | Where it lives                    | Separate files?                             |
| ----------------------- | --------------------------------- | ------------------------------------------- |
| **Subtitle tracks**     | Their own playlist and `.vtt` segments | Yes                                    |
| **Embedded captions**   | Inside the video stream itself    | No, and players handle them differently     |

---

## Part B: Playback States

A player is **always in one state**, and the **UI should follow it**.

| State              | Meaning                                  |
| ------------------ | ---------------------------------------- |
| **Idle / loading** | Source set, nothing ready yet            |
| **Buffering**      | Needs more data before it can continue   |
| **Ready**          | Enough data to start                     |
| **Playing**        | Frames are advancing                     |
| **Paused**         | Stopped by the viewer or the app         |
| **Ended**          | Reached the end of a VOD                 |
| **Error**          | Something failed                         |

> **Key point:** "playing" and "should be playing" are **different things**.
>
> A player can be set to play but be **buffering**, so the video is frozen while the app thinks it is playing. **Show a spinner for buffering** and don't rely on the play flag alone.

---

## Part C: Seeking

**Seeking** means **jumping to another position** on the timeline.

### What Actually Happens

1. The player works out **which segment** contains that time.
2. It **discards the old buffer**, since the position changed.
3. It **downloads the new segment(s)**, then resumes, which causes a **short buffering moment**.

### Things to Know

| Topic               | Detail                                                                                                                          |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| **Keyframes**       | Video can only start cleanly at a keyframe, so a seek often lands at a nearby point rather than the exact millisecond.          |
| **VOD vs live**     | In VOD you can seek anywhere. In live you can only seek within the **seekable window**: the sliding window of segments still in the playlist. |
| **Remote controls** | On TV, seeking is usually a **10-second skip** with the arrow keys. It should keep working on repeated presses **without piling up requests**. |
