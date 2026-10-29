# Tokens

A **token** is a **long random string** that proves **"this device is logged in as this user"**.

After the login, the backend gives the app a token, and the app **uses it instead of a password**.

## Two Rules

| Rule                                 | Why                                                                                                                                         |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------- |
| **1. Sent with every request**       | The backend **doesn't remember the app** between calls, so each request must carry the token to say **who is asking**                      |
| **2. Stored encrypted on the device** | The app has to **keep the token after it closes**, or the user would log in again on every launch. But the token is **as powerful as a password**, so it **must not sit in plain text** |

## With and Without a Token

```
App                                 Backend
│  GET /home                          │
│  Authorization: Bearer eyJhbGc...   │
│ ──────────────────────────────────► │  checks token → knows the user
│ ◄────────────── 200 + rails         │
│                                     │
│  GET /home   (no token)             │
│ ──────────────────────────────────► │
│ ◄────────────── 401 Unauthorized    │
```

| Request                 | Header                              | Response                |
| ----------------------- | ----------------------------------- | ----------------------- |
| **With token**          | `Authorization: Bearer eyJhbGc...`  | ✅ `200` + rails        |
| **Without token**       | (none)                              | ❌ `401 Unauthorized`   |

---

## Pros and Cons

### Sending the Token with Every Request

| ✅ Pros | ❌ Cons |
| ------- | ------- |
| **Simple**, and it works with **any backend endpoint** | If **one request path forgets the header**, that call fails with a `401` while the rest of the app works, which makes the bug **look random** |
| The backend can **identify the user**, apply **country rules**, and return **personal data** like Continue Watching | If the token **leaks in logs or screenshots**, someone else can **act as the user** |

### Storing the Token Encrypted

| ✅ Pros | ❌ Cons |
| ------- | ------- |
| The user **stays logged in** across app restarts | It is **more work than AsyncStorage**, and behavior **differs by platform and device** |
| **Another app or a stolen backup** can't easily read it | **Secure storage can fail** or return nothing |
