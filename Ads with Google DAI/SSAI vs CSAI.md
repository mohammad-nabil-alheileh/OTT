# SSAI vs CSAI

There are **two ways to get ads into a video**. The difference is **who inserts the ad**.

| Method                                | Who inserts the ad | How it works                                                                                                     |
| ------------------------------------- | ------------------ | ---------------------------------------------------------------------------------------------------------------- |
| **SSAI** (Server-Side Ad Insertion)   | The **server**     | Stitches the ads into the video stream itself. The app gets **one continuous stream** where ads and content are already joined |
| **CSAI** (Client-Side Ad Insertion)   | The **app**        | Requests ads separately, **pauses the content**, plays the ad **in its own player**, then **resumes** the content |

> **Google DAI is SSAI.**

```
SSAI:  Server ── [content + ad + content] ──▶ App (one stream)

CSAI:  App ── content ── pause ── [ad player] ── resume ── content
```

---

## SSAI

### ✅ Pros

- **Works on weak devices** like TVs, since the player just plays one stream
- **Ad blockers can't easily remove** the ads
- **No gap or buffering** between content and ad
- **Same code path** on every platform

### ❌ Cons

- The app **doesn't know where ads are** unless it is told
- **Two timelines** appear
- **Seeking and resume** get tricky
- **Depends on Google** being up

---

## CSAI

### ✅ Pros

- The app has **full control** and knows exactly when an ad starts and ends
- **Simple to build** the ad UI
- **Easier to pause, seek and resume**

### ❌ Cons

- Needs an **ad SDK per platform**
- **More work and more bugs** on TV devices
- **Can be blocked**
- **Visible gap or buffering** when switching between ad and content

---

## Side by Side

| Aspect                     | SSAI                          | CSAI                              |
| -------------------------- | ----------------------------- | --------------------------------- |
| **Weak devices (TVs)**     | ✅ Works well                 | ❌ More work and bugs             |
| **Ad blockers**            | ✅ Hard to block              | ❌ Can be blocked                 |
| **Ad ↔ content switch**    | ✅ No gap                     | ❌ Visible gap or buffering       |
| **Code across platforms**  | ✅ Same code path             | ❌ Ad SDK per platform            |
| **Knowing where ads are**  | ❌ Only if told               | ✅ Knows exactly                  |
| **Seek and resume**        | ❌ Tricky (two timelines)     | ✅ Easier                         |
| **Ad UI**                  | —                             | ✅ Simple to build                |
| **External dependency**    | ❌ Depends on Google being up | —                                 |
