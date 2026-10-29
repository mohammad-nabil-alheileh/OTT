# No Refresh Token: A 401 Signs the User Out

## Two Tokens in Many Apps

| Token             | Lifetime        | Used for                                                          |
| ----------------- | --------------- | ----------------------------------------------------------------- |
| **Access token**  | **Short-lived** | Sent with **every request**                                       |
| **Refresh token** | **Long-lived**  | Used only to **quietly get a new access token** when the old one expires |

## When There Is No Refresh Token

If an app has **no refresh token**, there is **only one token**. When the backend rejects it, the app **cannot fix that silently**. So the rule is simple:

> **If any request returns `401`, clear the stored token, sign the user out, and show the SignIn screen.**

## With vs Without a Refresh Token

```
With a refresh token                    Without one (this app)
────────────────────────────            ──────────────────────────────
GET /home → 401                         GET /home → 401
  → use refresh token                     → delete token
  → get new access token                  → show SignIn
  → retry GET /home → 200
  User notices nothing                    User has to log in again
```

| Step after a `401`  | With a refresh token        | Without one (this app)     |
| ------------------- | --------------------------- | -------------------------- |
| **1**               | Use the refresh token       | Delete the token           |
| **2**               | Get a new access token      | Show SignIn                |
| **3**               | Retry `GET /home` → `200`   | —                          |
| **What the user sees** | ✅ **Nothing**           | ❌ **Has to log in again** |

## Why a 401 Can Happen

| Cause                                     |
| ----------------------------------------- |
| The token **expired**                     |
| The token was **revoked**                 |
| The user **logged out on another device** |
