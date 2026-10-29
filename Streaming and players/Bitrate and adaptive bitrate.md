# Bitrate and Adaptive Bitrate

## Bitrate

**Bitrate** is **how much data per second** a video needs, measured in **bits per second**.

> More bitrate means a **sharper picture**, but the viewer's connection has to deliver it **fast enough**.

## Adaptive Bitrate (ABR)

Instead of one file, the video is **encoded several times at different qualities**. This set is called a **ladder** (each quality is a **rung**, or **rendition**):

| Rung | Resolution | Bitrate  |
| ---- | ---------- | -------- |
| 1    | 1080p      | 5 Mbps   |
| 2    | 720p       | 2.5 Mbps |
| 3    | 480p       | 1 Mbps   |
| 4    | 240p       | 400 kbps |

### How the Player Switches

While playing, the player **measures**:

- how fast data is arriving
- how full its buffer is

Then it **switches rungs automatically**:

| Situation                | What the player does | Result                                        |
| ------------------------ | -------------------- | --------------------------------------------- |
| **Connection drops**     | Steps down (e.g. to 480p) | Picture gets blurrier, but **keeps playing** |
| **Connection recovers**  | Steps back up        | Picture gets sharper again                    |
