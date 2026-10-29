# Blocked

When the backend says a video is **blocked by country**, the app shows a **blocked screen**. There are **three rules** for it:

| # | Rule                                      | In short                                                         |
| - | ----------------------------------------- | ---------------------------------------------------------------- |
| 1 | **The message**                           | "Unavailable due to rights restrictions"                         |
| 2 | **No Retry button**                       | Retrying always gets the same answer                             |
| 3 | **Country unknown has its own message**   | e.g. "We couldn't determine your location"                       |

---

## 1. The Message

> **"Unavailable due to rights restrictions"**

It explains that the block is about **licensing**, **not a fault in the app**.

| ✅ Pros | ❌ Cons |
| ------- | ------- |
| Tells the user the **app is working** and the limit is licensing, which means **fewer support complaints** | Doesn't say **which country rule applied** or **what the user can do**, since the app can't or shouldn't explain licensing details |

## 2. No Retry Button

Retrying sends the **same request from the same country** and gets the **same answer**. A Retry button would only invite **pointless taps**.

| ✅ Pros |
| ------- |
| It is **honest**: the user isn't led to believe the problem might fix itself |
| It **avoids repeated useless requests** |

## 3. Country Unknown Has Its Own Message

Sometimes the backend **can't work out the user's country at all**, for example when the **IP can't be looked up**. That is a **different situation from "blocked"**, so it needs **different wording**:

> **"We couldn't determine your location"**

| Situation           | Cause                                    | Message                                      |
| ------------------- | ---------------------------------------- | -------------------------------------------- |
| **Blocked**         | The country rule doesn't allow playback  | "Unavailable due to rights restrictions"     |
| **Country unknown** | The location lookup failed               | "We couldn't determine your location"        |

| ✅ Pros | ❌ Cons |
| ------- | ------- |
| **Points to the real cause**, so testers and support can tell a **location lookup failure** from a **real block** | In some flows it may be **unclear whether to block or allow** playback when the country can't be found. That is a **product decision to confirm** |
