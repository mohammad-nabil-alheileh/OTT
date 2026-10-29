# No Rewinding Live

**On-demand video is a file**, so you can jump anywhere in it.

**Live is different**: the stream is being produced **right now**, and our app **does not keep a recording of the past** that the user can scrub through.

## What This Means

| Action         | VOD          | Live                                                         |
| -------------- | ------------ | ------------------------------------------------------------ |
| **Rewind**     | ✅ Yes       | ❌ Can't see what aired 10 minutes ago                       |
| **Skip ahead** | ✅ Yes       | ❌ The future does not exist yet                             |
| **Seekbar**    | Moves freely | Stays **pinned at the live point**, the "edge" of the stream |

```
Past (not kept)  ─────────────────────▶ ● Live edge   (future doesn't exist yet)
```

## No DVR Window

This is sometimes called having **no DVR window**.

| Stream type                  | DVR window | Can rewind live? |
| ---------------------------- | ---------- | ---------------- |
| **Streams that allow it**    | ✅ Yes     | ✅ Yes           |
| **Our stream**               | ❌ No      | ❌ No            |

## Things to Keep in Mind

| Topic                                           | Detail                                                                                                    |
| ----------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| **Hide or disable controls that can't work**    | A draggable bar that does nothing **feels broken**                                                        |
| **Block seeking in the logic, not only the UI** | The UI is just **one way in**                                                                             |
| **`duration = -1` breaks a normal seekbar**     | It would have **no valid range**, which is another reason it **must not render for live**                 |
| **Pausing is different from rewinding**         | The user **can pause** live, and then **falls behind** the live point. This is why we need **"Go Live"** (see [Pause live](Pause%20live.md)) |
