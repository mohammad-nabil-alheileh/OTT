# API Traffic vs Video Traffic

## Two Kinds of Traffic

**API traffic** is **small JSON requests that ask questions**, such as:

- "What movies are in this row?"
- "Is this user allowed to watch?"
- "Where is the stream URL?"

**Video traffic** is **large, continuous downloads** of video data, split into **many small chunks (segments)**, fetched **over and over** while the video plays.

## Comparison

| Aspect      | API traffic                        | Video traffic                                     |
| ----------- | ---------------------------------- | ------------------------------------------------- |
| **Size**    | Small (KB)                         | Huge (MB per chunk, GB total)                     |
| **Format**  | JSON                               | `.m3u8` / `.mpd` manifest, then `.ts` / `.m4s` segments |
| **Server**  | Your backend (`api.example.com`)   | CDN edge (`cdn.example.com`)                      |
| **Pattern** | Request, response, done            | Continuous, every few seconds while playing       |
| **Needs**   | Low latency, correctness           | High, steady bandwidth                            |
| **Cached?** | Usually not (personalized)         | Heavily cached at the edge                        |
| **Auth**    | Token in a header                  | Often signed URLs or tokens in the URL            |

```
App ── small JSON ──▶ api.example.com   (backend)
Player ── segments, again and again ──▶ cdn.example.com   (CDN edge)
```

---

## How They Fail Differently

| Failure          | What you see                                               | Can your code catch it?                                       |
| ---------------- | ---------------------------------------------------------- | ------------------------------------------------------------- |
| **API fails**    | An **error in your fetch** or a **bad status code**        | ✅ Yes, your code can catch it and **show a message**         |
| **Video fails**  | The player **reports an error** or just **buffers forever** | ❌ Your fetch code **never sees it**, because the **player did the downloading** |

---

## Why It Matters on TV

| Reason                           | Detail                                                                                                                |
| -------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| **Bandwidth**                    | Video uses **far more bandwidth** than the API, so a **slow connection hurts video first**                           |
| **Constant stream**              | A brief network drop mid-playback causes a **buffering spinner**, while a brief drop for an API call just means **one retry** |
| **Different owners**             | Different teams often own each side, so **knowing which side broke tells you who to ask**                            |
