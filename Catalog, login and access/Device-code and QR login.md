# Device-Code and QR Login

Typing an email and password **with a TV remote is slow and painful**. So TV apps usually let the user **log in on another device**, such as their phone, and the **TV picks up the result**.

> **Key idea:** the **TV never sees the password**. The user signs in on the phone, and the backend **links that sign-in to the TV's waiting request**.

## Two Ways to Start

| Method                | What the TV shows                                        | What the user does                                                    | Typing needed? |
| --------------------- | -------------------------------------------------------- | --------------------------------------------------------------------- | -------------- |
| **Device-code login** | A **short code** and a **URL**                           | Opens the URL on their phone or laptop, signs in, and **types the code** | ✅ Yes (the code) |
| **QR login**          | A **QR code** containing the URL and code together       | **Scans it** with their phone camera                                  | ❌ Nothing to type |

## The Flow

```
TV                           Backend                      Phone
│                               │                            │
│ 1. "Start login"              │                            │
│ ────────────────────────────► │                            │
│ ◄─ deviceCode + userCode      │                            │
│    + expiresIn + interval     │                            │
│                               │                            │
│ 2. Show "ABCD-1234" + QR      │                            │
│                               │  3. User opens URL, signs  │
│ 4. Poll: "approved yet?"      │ ◄───────── in, enters code │
│ ────────────────────────────► │                            │
│ ◄─ "pending" (repeat)         │                            │
│ ────────────────────────────► │                            │
│ ◄─ "approved" + tokens        │                            │
│                               │                            │
│ 5. Save tokens, go Home       │                            │
```

| Step | Who      | What happens                                                                      |
| ---- | -------- | --------------------------------------------------------------------------------- |
| 1    | **TV**   | Asks the backend to **start login**, and gets back `deviceCode`, `userCode`, `expiresIn` and `interval` |
| 2    | **TV**   | Shows the code (e.g. `ABCD-1234`) and a QR code                                   |
| 3    | **Phone** | User opens the URL, **signs in**, and enters the code                            |
| 4    | **TV**   | **Polls** the backend: "approved yet?" It gets `pending` until the user finishes, then `approved` + **tokens** |
| 5    | **TV**   | **Saves the tokens** and goes to Home                                             |

### What the Backend Sends at the Start

| Field          | Meaning                                                    |
| -------------- | ---------------------------------------------------------- |
| `deviceCode`   | The TV's own ID for this login attempt, used when polling  |
| `userCode`     | The short code shown to the user (e.g. `ABCD-1234`)        |
| `expiresIn`    | How long the code stays valid                              |
| `interval`     | How often the TV should poll                               |
