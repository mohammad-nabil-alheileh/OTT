# Ad UI

With **SSAI** the player **has no idea an ad is playing**, so **your app builds the ad UI itself** from the **break times Google returned**.

## The Four Parts

| # | Part                              | What it does                                                                                     |
| - | --------------------------------- | ------------------------------------------------------------------------------------------------ |
| 1 | **Skip button**                   | Shown during an ad, usually **after a few seconds**                                              |
| 2 | **"Why this ad"**                 | A small link/icon that explains why the viewer sees this ad. It is a **Google requirement**, not optional decoration |
| 3 | **Yellow markers on the seekbar** | Small marks showing **where the ad breaks are**, so the viewer knows an ad is coming             |
| 4 | **Seeking blocked in ads**        | While an ad plays, the **seekbar is disabled** so the viewer can't drag through it               |

```
Seekbar:  ●━━━━━━━━━|━━━━━━━━━━━━━━|━━━━━━━━━━━━|━━━━━
                    ▲              ▲            ▲
             yellow markers = ad breaks
```

## On TV

> **One extra issue:** all of these controls must be **reachable with the remote**, so **each one needs to be focusable**.
