# Content and Playback APIs

Your backend APIs split into **two groups**, based on the **question they answer**.

## The Two Groups

### Content APIs

> **"What is there to watch?"**

They return the **catalog**:

- home screen rows
- movie details
- search results
- titles and descriptions
- poster image URLs

They are **safe to show to anyone** and are **heavily cached**.

### Playback APIs

> **"Can this user watch this title right now, and where is the stream?"**

They return:

- the **stream URL**
- **DRM license** info
- **subtitle tracks**
- the **resume position**

They are **personal**, **short-lived**, and **never cached for long**.

## Comparison

| Aspect               | Content API                          | Playback API                          |
| -------------------- | ------------------------------------ | ------------------------------------- |
| **Question**         | What can I browse?                   | Can I play this, and where?           |
| **Example endpoint** | `GET /v1/home`, `GET /v1/movies/123` | `POST /v1/movies/123/playback`        |
| **Personalized?**    | Somewhat (recommendations)           | Always (account, device, region)      |
| **Cacheable?**       | ✅ Yes, for minutes or hours         | ❌ No, or only for seconds            |
| **When it's called** | On every screen                      | When the user presses Play            |
| **If it fails**      | Empty screen or missing posters      | "Can't play this title"               |
| **Returns**          | Metadata, image URLs                 | Stream URL, tokens, DRM, subtitles    |

```
Browse screens ── Content API ──▶ rows, posters, details
Press Play     ── Playback API ─▶ stream URL, DRM, subtitles, resume position
```

---

## Why It Matters on TV

| API              | Detail                                                                                                                              |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| **Content API**  | Runs **constantly while the user scrolls** with the remote, so slow responses make the **whole UI feel laggy**. **Prefetch and cache** them |
| **Playback API** | Runs **once per Play press**, so a slow one directly delays **"time to first frame"**, which users notice immediately              |

> Many TV bugs are **"the poster shows but the video won't play"**. That means the **content API worked** and the **playback API failed**.
