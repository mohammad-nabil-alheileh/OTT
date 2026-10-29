# Error Conventions, Retries, Versioning, Feature Flags

| # | Topic               | In one line                                                         |
| - | ------------------- | ------------------------------------------------------------------- |
| 1 | **Error conventions** | The backend always reports failures **in the same shape**          |
| 2 | **Retries**         | Try again **only** when the failure is temporary                    |
| 3 | **Versioning**      | The backend keeps **old API versions alive** for old apps           |
| 4 | **Feature flags**   | **On/off switches** controlled by the backend, not by an app release |

---

## 1. Error Conventions

A **convention** is an agreement: **"when something fails, the backend always reports it in the same shape."**

> Without it, every endpoint would fail in a different way and your app would need **special code for each**.

### Two Layers

| Layer                 | What it is                                       | Example                                          |
| --------------------- | ------------------------------------------------ | ------------------------------------------------ |
| **HTTP status code**  | The **broad category**                           | `4xx` = the request was wrong or not allowed<br>`5xx` = the server failed |
| **Error body**        | A **stable, machine-readable code** plus a **message** | `{ "code": "NOT_ENTITLED", "message": "..." }` |

---

## 2. Retries

Some failures are **temporary** (a network blip, a busy server). Trying again often works. But **retrying the wrong failure only makes things worse**.

| ✅ Retry                                    | ❌ Do not retry                         |
| ------------------------------------------ | -------------------------------------- |
| Network errors                             | `401`                                  |
| Timeouts                                   | `403`                                  |
| `503`                                      | `404`                                  |
| `429` (too many requests, **wait first**)  | `NOT_ENTITLED`                         |
|                                            | Asking again gives **the same answer** |

> Good retries **wait longer each time** (**exponential backoff**) instead of hammering the server.

```
fail → wait 1s → retry → fail → wait 2s → retry → fail → wait 4s → retry ...
```

---

## 3. Versioning

**Old versions of your app stay installed on TVs for months or years.** If the backend changes a response shape, **old apps break**.

So the **API carries a version**, and the **backend keeps old versions alive**.

```
Old TV app  ── GET /v1/home ──▶ backend (v1 shape, still supported)
New TV app  ── GET /v2/home ──▶ backend (v2 shape)
```

---

## 4. Feature Flags

A **feature flag** is an **on/off switch** (or a setting) **controlled by the backend**, not by an app release. The app asks **"is this feature on?"** and behaves accordingly.

### Uses

| Use                          | Example                                                                                     |
| ---------------------------- | ------------------------------------------------------------------------------------------- |
| **Gradual rollout**          | Roll out a feature to **5% of users first**, then everyone                                  |
| **Kill switch**              | **Turn off a broken feature instantly**, without waiting for TV app store approval          |
| **Targeting**                | Enable something only for **certain devices or regions**, like a codec that only works on newer TVs |

---

## When Playback Fails, All Four Show Up

| Topic                 | Role in a playback failure                                   |
| --------------------- | ------------------------------------------------------------ |
| **Error code**        | Tells you **what went wrong**                                |
| **Retry**             | **May fix it** if it was temporary                           |
| **Version**           | Decides **which response shape** your app expects            |
| **Flag**              | May decide **which player or stream format** is used         |
