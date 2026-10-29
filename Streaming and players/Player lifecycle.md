# Player Lifecycle

| Part | Topic           |
| ---- | --------------- |
| A    | Player lifecycle |
| B    | Controls        |
| C    | Remote keys     |
| D    | Cleanup         |

---

## Part A: Player Lifecycle

```
Create → Load → Use → (Change source → Load → Use ...) → Destroy
```

| Stage             | What happens                                                                                          |
| ----------------- | ----------------------------------------------------------------------------------------------------- |
| **Create**        | The player instance is made when the screen mounts                                                    |
| **Load**          | We give it the URL, and it fetches playlists and the first segments                                   |
| **Use**           | Play, pause, seek, change tracks                                                                      |
| **Change source** | The viewer picks another episode. The old stream **must be fully stopped** before the new one starts |
| **Destroy**       | The screen unmounts, and the player **must release its resources**                                   |

---

## Part B: Controls

The controls are **UI** (play/pause button, progress bar, subtitle menu) **driving the player** and **reflecting its state**.

> **Key idea: one source of truth.** The player reports state, our UI displays it, and button presses change it.

```
Player ── reports state ──▶ UI displays it
  ▲                              │
  └──── button presses change it ┘
```

### Things to Handle

| Topic                | Detail                                                                                          |
| -------------------- | ----------------------------------------------------------------------------------------------- |
| **Auto-hide**        | Controls disappear after a few seconds of no input and reappear on any key press               |
| **Progress updates** | `onProgress` fires often, so updating heavy UI on every tick can **slow weak TVs**             |
| **Disabled states**  | Don't allow seeking while loading, or beyond the seekable window on live                       |

---

## Part C: Remote Keys

```js
useTVEventHandler((evt) => {
  if (evt.eventType === 'select')    togglePlay();
  if (evt.eventType === 'right')     seekBy(+10);
  if (evt.eventType === 'left')      seekBy(-10);
  if (evt.eventType === 'playPause') togglePlay();
});
```

> That hook is the **React Native TV** one, and **names differ by platform**. Samsung and LG web builds receive **keyboard-style events** with **platform-specific key codes**, which usually need mapping to a common set.

### Points to Remember

| Topic                    | Detail                                                                                              |
| ------------------------ | --------------------------------------------------------------------------------------------------- |
| **Back key**             | Must **exit the player cleanly**, not leave the stream running in the background                   |
| **Held keys**            | Holding right to skip can fire many events, so **debounce seeks**                                  |
| **Focus**                | On TV, one element has focus at a time. If the controls aren't focused, key presses may go to the wrong place |
| **Platform differences** | The same physical button can report a **different key code** on each TV brand                      |

---

## Part D: Cleanup

**Cleanup** means **releasing everything the player used**.

### What to Clean Up

| Cleanup step                                      | Why it matters                                                                                       |
| ------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| **Stop and destroy the player instance**          | Frees the decoder, which matters because TVs may allow **only one**                                 |
| **Remove event listeners**                        | So old players can't call into a screen that no longer exists                                       |
| **Cancel timers**                                 | Such as the auto-hide timer or progress polling                                                     |
| **Abort in-flight network requests**              | For segments                                                                                        |

### Symptoms of Missing Cleanup

- The **decoder is still busy**, so the next video fails to start or plays black.
- **Audio keeps playing** after leaving the screen.
- **Memory grows** each time a video is opened, until the TV slows down or the app is killed.
- **Callbacks from the old player** update state on an unmounted screen.
