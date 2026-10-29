# App vs Player

> The **app** sends commands and shows the UI; the **player** decodes the video.

## Comparison

| Aspect          | App (React Native code)                                                                                           | Player (native video engine)                                                                  |
| --------------- | ----------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| **Main job**    | Decide what to play and show the UI                                                                               | Actually play it                                                                              |
| **Owns**        | Screens, navigation, remote/focus handling, catalog, login, buttons, progress bar, spinners, error messages      | Downloading the manifest and segments, buffering, ABR, decoding, DRM, drawing frames, audio   |
| **Knows about** | Your data: titles, user, ad rules, analytics                                                                      | The stream: bitrate, buffer, codecs, timing                                                   |

## Two Directions of Communication

```
App  ── commands ──▶  Player
App  ◀── events ───  Player
```

| Commands go down (app → player)    | Events come up (player → app)        |
| ---------------------------------- | ------------------------------------ |
| Load this source                   | Loaded (duration is now known)       |
| Play / pause                       | Progress (current time, every so often) |
| Seek to a position                 | Buffering started / ended            |
| Select an audio or subtitle track  | Ended                                |
| Change volume, mute                | Error                                |
| Stop                               |                                      |
