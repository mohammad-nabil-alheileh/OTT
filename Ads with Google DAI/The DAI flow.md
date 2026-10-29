# The DAI Flow

**Ask Google for a stream with ads in it.** The only thing that changes is **what you send**, and that depends on whether the content is **live** or **on-demand**.

## What You Send

| Content type                         | What you send                     | What it identifies                                                              |
| ------------------------------------ | --------------------------------- | ------------------------------------------------------------------------------- |
| **Live** (channels, events)          | **Asset key**                     | The live stream in Google Ad Manager                                            |
| **On-demand** (movies, episodes)     | **Content source ID + video ID**  | Content source ID = your **whole library**<br>Video ID = the **one title**      |

## The Flow

```
App                                        Google DAI
 │  1. Stream request                          │
 │     live:  asset key                        │
 │     VOD:   content source ID + video ID     │
 │ ──────────────────────────────────────────► │
 │                                             │  2. Google picks ads, stitches
 │                                             │     them into the content
 │  3. Response: stream URL + ad-break times   │
 │ ◄────────────────────────────────────────── │
 │  4. Player plays the URL                    │
```

| Step | Who            | What happens                                         |
| ---- | -------------- | ---------------------------------------------------- |
| 1    | **App**        | Sends the stream request (asset key, or content source ID + video ID) |
| 2    | **Google DAI** | Picks ads and stitches them into the content         |
| 3    | **Google DAI** | Responds with a **stream URL + ad-break times**      |
| 4    | **App**        | The player plays the URL                             |

---

## Pros and Cons

### Asset Key (Live)

| ✅ Pros                                          | ❌ Cons                                                                                |
| ----------------------------------------------- | ------------------------------------------------------------------------------------- |
| **One value per channel**, simple request       | If the key is wrong or the channel is misconfigured, there is **no stream**          |
| Google **tracks the live ad breaks** for you    | You **can't seek** to a specific content position the way you can in VOD             |

### Content Source ID + Video ID (VOD)

| ✅ Pros                                                                                                  | ❌ Cons                                                              |
| ------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| Ad breaks can be **planned in advance**                                                                 | **Two values** must both be correct                                 |
| **One content source ID covers the whole catalog**, so only the video ID changes per title             | A **wrong video ID** usually means a failed request or no ads       |

### The Flow as a Whole

| ✅ Pros                                                                     | ❌ Cons                                                                                         |
| -------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| Ad decisions, stitching and tracking **happen on Google's side**           | The app **depends on a network call** before playback can start, which **adds startup delay** |
| The app **only sends a small request**                                     | **If Google fails**, you need a **fallback**                                                   |
