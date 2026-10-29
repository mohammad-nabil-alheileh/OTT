# Shaka Player and the Web Shim

## What Is a Shim?

A **shim** is a **small adapter layer** that pretends to be one thing while using another underneath.

In our web build, the **bundler is configured** so that when the code imports `react-native-video`, it gets **our shim** instead.

> The **import is the same**, so the app code doesn't change. Only **what it resolves to** changes. This is usually done with a **bundler alias**.

```
App code: import Video from 'react-native-video'
        │
        ├── Android / tvOS → real react-native-video
        └── Web (bundler alias) → our shim → Shaka Player → <video>
```

## What Shaka Does Behind the Shim

1. **Downloads** the master playlist and the media playlists.
2. **Chooses a rendition** (ABR) and downloads segments.
3. **Appends the segment bytes** to the browser's `<video>` through **Media Source Extensions (MSE)**.
4. **Handles** subtitles, track switching and retries.

## Who Does What

| Layer                    | Job                                                    |
| ------------------------ | ------------------------------------------------------ |
| **Our shim**             | Translates our props and callbacks into Shaka calls    |
| **Shaka Player**         | Playlists, ABR, segments, subtitles, tracks, retries   |
| **Browser `<video>`**    | Only the **final decoding and drawing**                |

> On **Samsung and LG**, that decoding is done by the **TV's own hardware**.
