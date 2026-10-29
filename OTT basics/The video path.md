# The Video Path

How a video gets from the original file to the viewer's screen:

```
Source file → Encode → Package → CDN → Player → Screen
```

## 1. Encode

The original video file is **huge**. Encoding **compresses** it using a **codec**.

It is also done **several times**, to create different versions of the same video, called **renditions**:

| Rendition  | Resolution | Bitrate (approx.) |
| ---------- | ---------- | ----------------- |
| **High**   | 1080p      | 5 Mbps            |
| **Medium** | 720p       | 3 Mbps            |
| **Low**    | 480p       | 1 Mbps            |

## 2. Package

Packaging **cuts each rendition into small segments** and creates a **manifest**: a text file that lists the renditions and where every segment is.

The two common formats:

| Format   | Manifest file | Typical use                                |
| -------- | ------------- | ------------------------------------------ |
| **HLS**  | `.m3u8`       | Apple devices, and widely supported on TVs |
| **DASH** | `.mpd`        | Android TV and many smart TVs              |

## 3. CDN (Content Delivery Network)

A CDN is a **network of servers around the world** that keep **copies of the segments**.

> A viewer downloads from a **nearby server** instead of from your one origin server far away.

## 4. Player

The player is the **software on the device** that does the actual watching work:

1. **Downloads** the manifest.
2. **Picks** a rendition that fits the current connection speed.
3. **Downloads segments** a few seconds ahead.
4. **Decodes** them, usually with the TV's hardware decoder, and shows them.
5. **Keeps measuring** the connection and **switches renditions** when it changes.
