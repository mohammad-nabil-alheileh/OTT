# Server-Driven Home

In a **server-driven Home**, the app **does not hard-code which rails to show**. It **asks the backend for a layout**, and the backend replies with a **list of rails**:

- **which** ones
- in what **order**
- with what **titles**
- with what **content**

> The app's job is to **render whatever comes back**.

## Compare the Two Approaches

```
Hard-coded Home (client decides)        Server-driven Home (backend decides)
─────────────────────────────────       ─────────────────────────────────────
App code says:                          App asks: GET /home
  1. show "Trending"                    Backend replies with the rails:
  2. show "Comedy"                        1. "Trending"
  3. show "Continue Watching"             2. "New this week"
                                          3. "Continue Watching"
Changing it = new app release           Changing it = backend change only
```

| Aspect                | Hard-coded Home       | Server-driven Home        |
| --------------------- | --------------------- | ------------------------- |
| **Who decides rails** | The client (app code) | The backend               |
| **How the app gets them** | Written in the code | `GET /home`             |
| **Changing the layout** | New app release     | Backend change only       |

> The app only needs to know **how to draw each kind of rail**. The backend **chooses which ones to send**.

---

## Pros and Cons

### ✅ Pros

| Pro                                  | Why                                                                          |
| ------------------------------------ | ---------------------------------------------------------------------------- |
| **No app release needed**            | Add, remove, or reorder rails freely. This matters because **store reviews take days** |
| **Personalization**                  | The backend can send different rails to different **users, countries, or devices** |
| **Experiments**                      | **A/B tests** on Home layout are easy to run                                 |
| **One layout, many platforms**       | Phone, TV, and web can **share the same backend logic**                      |

### ❌ Cons

| Con                                  | Why                                                                                              |
| ------------------------------------ | ------------------------------------------------------------------------------------------------ |
| **Can't show Home without the backend** | If the request fails, you need a **fallback or an error screen**                              |
| **Harder to test**                   | Two users can see different Homes, so "it looks different on my device" is **not automatically a bug** |
| **Unknown types can break old app versions** | If the app doesn't **handle them gracefully**                                            |
| **More work up front**               | The app needs **generic components** instead of hard-coded screens                               |
