# Pause Live and "Go Live"

While the user is **paused**, the real broadcast **keeps going**. When they press play, the video **resumes from where they paused**, so they are now **behind the live point** by however long they were paused.

```
Paused here ●─────── (broadcast keeps going) ───────▶ ● Live edge
            └──────── user is this far behind ────────┘
```

## How the App Shows It

| UI element         | What it shows                                                                                          |
| ------------------ | ------------------------------------------------------------------------------------------------------ |
| **LIVE badge**     | 🔴 **Red / active** = "you are at the live point"<br>⚪ **Grey** = "you are behind"                    |
| **Go Live action** | Lets the user **jump back to the live point**. In our app it **reloads the stream** instead of seeking |

## Why Go Live Reloads Instead of Seeking

| Reason                   | Explanation                                                                                                                         |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------- |
| **No DVR window**        | Seeking needs a timeline with a past you can move around in. Our live stream has none, so there is **no valid position to seek to** |
| **Buffered data is old** | Jumping within it would only land on **stale video**                                                                                |
| **Reload joins fresh**   | Loading the stream URL again joins the broadcast **fresh at the live edge**, which is exactly what "Go Live" means                  |

## Things to Keep in Mind

| Topic                                   | Detail                                                                                            |
| --------------------------------------- | ------------------------------------------------------------------------------------------------- |
| **State tells the UI the truth**        | `isBehindLive` drives **both** the grey badge and the Go Live button, so they **cannot disagree** |
| **Pausing alone marks you as behind**   | Without a DVR window, the app **cannot measure how far behind** you are, so **any pause counts**  |
| **Reload means a short loading moment** | **Show a spinner**, because the video restarts                                                    |
| **Fetch a fresh stream URL**            | If the backend uses **short-lived or signed URLs**, reusing the old one may fail                  |
