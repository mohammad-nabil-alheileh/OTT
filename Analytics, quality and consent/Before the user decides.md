# Before the User Decides

## Why "Dropped" and Not "Queued"

| Option              | What happens                                                    | Problem                                                                                                         |
| ------------------- | --------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| ✅ **Drop**         | Events are **discarded** until consent is granted               | Data is lost, but it is the **legally clean** option                                                            |
| ⚠️ **Queue, then send** | Events are **stored on the device**, and sent after acceptance | You have **collected and stored data before consent**. Many teams treat this as **risky**, so **ask your legal team** |
| ❌ **Send anyway**  | Events **go out immediately**                                   | **Clearly a violation** in opt-in regions                                                                       |

---

## Why Youbora Is a Special Case

**Youbora tracks a whole video session**: start, buffering, quality, end. A session has a **clear beginning**, so it **can't be switched on halfway** and still be accurate.

```
Video:     start ──────────────────────────────────────── end
Consent:   (off) ──────── user accepts ────────────────── (on)
Youbora:   no session      └── late session (first part missing) ──
```

| Situation                                  | What happens to the Youbora session                                                                 |
| ------------------------------------------ | --------------------------------------------------------------------------------------------------- |
| **Youbora is off when the video starts**   | **No session** is created                                                                           |
| **User accepts during playback**           | A session **can start late**, and the **first part of the video is missing**                        |

> Whether your app **starts it late** or **waits for the next video** depends on **your implementation**.

---

## Troubleshooting: Missing Data and Consent

| What you see                                    | Possible consent cause                                         |
| ----------------------------------------------- | -------------------------------------------------------------- |
| **No events from some users at all**            | They **declined**, or **never answered** the popup             |
| **Youbora has no sessions for new installs**    | Youbora was **off while the video played**                     |
| **Sudden drop in events after a release**       | The **popup, vendor mapping or the Didomi config** changed     |
| **Events are fine in QA but low in production** | **Testers accept** the popup. **Real users often don't**       |
| **Numbers differ between regions**              | **Opt-in (GDPR)** versus **opt-out (CPRA)** defaults           |
| **Events missing on Apple TV only**             | The **ATT** answer                                             |
| **First video of every session is missing**     | The **popup was still open** when it started                   |
