# A Successful API Call Does Not Mean the Video Will Play

A **`200 OK`** from the playback API only means **the backend answered your question**. It does **not** mean the video bytes will **arrive, decrypt, or decode**.

> **Playback is a chain, and the API is only the first link.**

```
Playback API (200 OK) → CDN delivers segments → Network carries them → Player decrypts & decodes → Picture on screen
```

## Why the API Succeeds but the Video Fails

| # | Cause                              | What happens                                                                                                                  | Where it breaks     |
| - | ---------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- | ------------------- |
| 1 | **Expired or invalid stream token** | The API gave a signed URL, but it **expired** (long pause, wrong TV clock) or was **malformed**. The CDN returns **`403`**   | **CDN**             |
| 2 | **CDN or edge problem**            | The edge is **down**, the segment is **missing (`404`)**, or the **region is blocked**. The API doesn't know                 | **CDN**             |
| 3 | **Unsupported format**             | The stream uses a **codec, resolution, or HDR mode** that this TV can't decode                                               | **Player / device** |
| 4 | **Network too slow**               | Everything is valid, but segments **arrive too slowly**, so you get **endless buffering**                                    | **Network**         |
| 5 | **"Soft" API errors**              | The API returns `200`, but the body says `{ "error": "NOT_ENTITLED" }` or an **empty `streamUrl`**, and the app **doesn't check** | **Your code**   |

---

## Why It Matters on TV

| Reason                       | Detail                                                                                                    |
| ---------------------------- | --------------------------------------------------------------------------------------------------------- |
| **Device variety**           | TVs have **many different chips and codec support**, so the same stream plays on one model and fails on another |
| **Wrong clocks**             | TV clocks are **often wrong**, which makes **signed tokens look expired**                                 |
| **No console**               | There's no console on a TV, so you **must log player events yourself**                                    |
| **Users see a black screen** | Users don't see "API succeeded". They see a **black screen**, so the app must **show a useful message or retry** |
