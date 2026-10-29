# Where a Player Bug Can Live

## The Three Places

| # | Layer                          | Platforms                  | What goes wrong                                                                                     |
| - | ------------------------------ | -------------------------- | --------------------------------------------------------------------------------------------------- |
| 1 | **The native player itself** (ExoPlayer/Media3, AVPlayer, or Shaka) | All                        | The player library has a bug, handles your stream in a way you don't expect, or the device's decoder fails |
| 2 | **Our react-native-video fork** | Android TV, Apple TV       | Bugs in the native wrapper code between React Native and the player                                  |
| 3 | **The Shaka shim**             | Web, Samsung, LG           | Translation layer bugs: a prop never implemented, an event mapped wrongly, or cleanup missing        |

### Which Two Layers per Platform

Every platform has **two layers** involved: a wrapper and a native player.

| Platform                 | Wrapper layer             | Native player       |
| ------------------------ | ------------------------- | ------------------- |
| **Android TV**           | react-native-video fork   | ExoPlayer / Media3  |
| **Apple TV**             | react-native-video fork   | AVPlayer            |
| **Web / Samsung / LG**   | Shaka shim                | Shaka Player        |

---

## A Debugging Routine

1. **Which platform?**
   That tells you **which two layers** are involved.

2. **Does the stream play elsewhere?**
   Open the master URL in Chrome and try a **reference player**.
   > If it fails everywhere, **stop looking in our code**.

3. **Does it fail on other platforms?**
   A bug on **only one platform** narrows the layer a lot.

4. **Check the events.**
   Log what the **player reports** and what the **wrapper passes to the app**.
   > If the player reports the right thing but the app sees something different, the bug is in the **translation layer**.

5. **Reproduce in Chrome** if it's a web-side bug.
   **DevTools** show requests, errors and Shaka logs.
