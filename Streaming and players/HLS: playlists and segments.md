# HLS: Playlists and Segments

**HLS (HTTP Live Streaming)** is a way to deliver video over **plain HTTP**. The video is cut into **segments**, and text files called **playlists** tell the player what exists and in what order.

> Because it's just HTTP, **any normal web server or CDN** can serve it.

## The Two Kinds of Playlist

| Playlist                 | How many         | What it lists          | Notes                          |
| ------------------------ | ---------------- | ---------------------- | ------------------------------ |
| **1. Master playlist**   | One per video    | The renditions         | This is the URL the app is given |
| **2. Media playlist**    | One per rendition | The actual segments   |                                |

```
Master playlist
├── Media playlist (1080p) → segment 1, segment 2, segment 3, ...
├── Media playlist (720p)  → segment 1, segment 2, segment 3, ...
└── Media playlist (480p)  → segment 1, segment 2, segment 3, ...
```

## How Playback Flows

1. The player **downloads the master playlist**.
2. It **picks a rendition**, usually a low one first for a fast start.
3. It **downloads that rendition's media playlist**.
4. It **downloads segments one by one** and feeds them to the decoder.
5. While playing, it **measures download speed** and may **switch** to another rendition's playlist.

## Segment Formats

| HLS version | Segment format          | Notes                   |
| ----------- | ----------------------- | ----------------------- |
| **Older**   | `.ts` (MPEG-TS)         |                         |
| **Newer**   | `.m4s` / fMP4           | Can be shared with DASH |

## HLS vs DASH

**DASH** is the other major adaptive streaming format. It does the **same job as HLS**, but with a different manifest file.

| Format   | Manifest file |
| -------- | ------------- |
| **HLS**  | `.m3u8`       |
| **DASH** | `.mpd`        |

| Platform          | Formats                |
| ----------------- | ---------------------- |
| **Apple**         | Prefers HLS            |
| **Android / Web** | Handle both HLS and DASH |
