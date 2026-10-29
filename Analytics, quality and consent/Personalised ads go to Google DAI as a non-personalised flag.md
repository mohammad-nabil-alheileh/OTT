# Personalised Ads Go to Google DAI as a Non-Personalised Flag

## Google DAI

**Google DAI (Dynamic Ad Insertion)** is part of **Google Ad Manager**. It uses **server-side ad insertion (SSAI)**: the ads are **stitched into the video stream on the server**, so the app receives **one continuous stream** of content and ads, with **no switching between two players**.

## Personalised vs Non-Personalised Ads

| Ad type                 | Targeted using                                                         |
| ----------------------- | ---------------------------------------------------------------------- |
| **Personalised**        | The viewer's **behaviour and identifiers**                             |
| **Non-personalised**    | Only **coarse context**: the content being watched, the rough location and the time |

## What the App Sends

| User choice                       | What the app sends to DAI              | What the viewer sees               |
| --------------------------------- | -------------------------------------- | ---------------------------------- |
| **Accepted** personalised ads     | No restriction flag                    | Ads **targeted to them**           |
| **Declined** or **not decided yet** | **Non-personalised flag** (`npa=1`)  | Ads **still play**, but **untargeted** |

```
Consent choice → stream request to DAI (with or without npa=1) → stitched stream with ads
```

---

## Important Details

### The Flag Is Set When the Stream Is Requested

Ads are **stitched in on the server**, so if the user **changes their consent mid-playback**, the **current stream keeps its old setting**. The new choice applies **from the next stream request**.

> **Decide** whether your app **restarts the stream** or **waits for the next video**.

| When consent changes      | Current stream          | Next stream request     |
| ------------------------- | ----------------------- | ----------------------- |
| **Mid-playback**          | Keeps the **old** setting | Uses the **new** setting |

### No Answer Yet Counts as Non-Personalised

This matches the **safe rule: unknown means no**.

> If the stream request fires **before the popup is resolved**, send **`npa=1`**.

### Revenue Effect

**Non-personalised ads usually earn less**, which is why **declining users reduce ad income**.
