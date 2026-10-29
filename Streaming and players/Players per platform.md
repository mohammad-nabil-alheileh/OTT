# Players per Platform

The app has **one `<Video>` component** in the code, but a **different real player** does the work on each platform.

> **react-native-video is a wrapper**: it asks the platform's own player to do the job.

```
<Video> (react-native-video)
├── Android TV        → ExoPlayer / Media3
├── Apple TV (tvOS)   → AVPlayer
└── Samsung / LG / Web → Shaka Player
```

## Which Player Runs Where

| Platform            | Player doing the work  |
| ------------------- | ---------------------- |
| **Android TV**      | ExoPlayer / Media3     |
| **Apple TV (tvOS)** | AVPlayer               |
| **Samsung (Tizen)** | Shaka Player           |
| **LG (webOS)**      | Shaka Player           |
| **Web (Chrome)**    | Shaka Player           |

---

## ExoPlayer / Media3 (Android and Android TV)

**Google's open-source media player** for Android.

**Media3** is its newer home: ExoPlayer was moved into the **Jetpack Media3** library.

**What it does:** HLS, DASH, subtitles, DRM, track selection, ABR, all **built in** and **configurable from the app side**.

## AVPlayer (Apple Platforms)

**Apple's built-in player.**

HLS is **Apple's own format**, so AVPlayer handles it **natively and very reliably**.

## Shaka Player (Web, Samsung and LG)

**Google's open-source JavaScript player.** It runs in a browser using the browser's **Media Source Extensions (MSE)**:

1. Shaka **downloads the playlists and segments** itself.
2. It **feeds the bytes** to the browser's `<video>` element.

---

## Comparison

| Aspect              | ExoPlayer / Media3     | AVPlayer             | Shaka             |
| ------------------- | ---------------------- | -------------------- | ----------------- |
| **Language**        | Java/Kotlin (native)   | Swift/Obj-C (native) | JavaScript        |
| **HLS**             | ✅ Yes                 | ✅ Yes               | ✅ Yes            |
| **DASH**            | ✅ Yes                 | ❌ No                | ✅ Yes            |
| **Configurability** | High                   | Low                  | High              |
| **Main risk**       | Device variety         | Strictness           | Weak TV browsers  |
