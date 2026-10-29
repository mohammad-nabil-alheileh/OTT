# A Dead Login

A **dead login** means the app **still looks logged in**, but the **backend no longer accepts the token**.

A `401` **should sign the user out**. But sometimes the sign-out **doesn't happen**, and the user sees **confusing, half-empty screens** instead of SignIn.

## Why It Happens

**Logged-in features fail quietly:**

| Screen / feature      | What happens with a dead login                                            |
| --------------------- | ------------------------------------------------------------------------- |
| **Account tab**       | The profile request fails, so the tab shows **nothing or a blank profile** |
| **Continue Watching** | The rail needs a user, so a failed request means the rail is **simply missing** |
| **Home**              | **Still loads**, because public rails don't need a login                  |

## Missing Is Not the Same as Empty

> **Key idea:** "missing" is **not** the same as "empty". On screen, **both look identical**.

| User                       | Continue Watching | Why                         |
| -------------------------- | ----------------- | --------------------------- |
| **User with no history**   | Empty             | There is nothing to show    |
| **User with a dead login** | Missing           | The **request failed**      |
