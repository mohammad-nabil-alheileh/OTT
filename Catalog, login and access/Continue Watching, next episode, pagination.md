# Continue Watching, Next Episode, Pagination

| Topic                 | In one line                                                    |
| --------------------- | -------------------------------------------------------------- |
| **Continue Watching** | A rail of things the user started but hasn't finished          |
| **Next episode**      | What the app plays or suggests when an episode ends            |
| **Pagination**        | Loading a long list in pieces instead of all at once           |

---

## Continue Watching

**Continue Watching** is a **rail** of things the user **started but hasn't finished**.

- The **backend stores a progress position** per user per video.
- The **app sends updates** while the user watches.
- A tile shows a **progress bar** and **resumes from where the user stopped**.

| ✅ Pros | ❌ Cons |
| ------- | ------- |
| **Brings users back** to content quickly | Needs **frequent progress writes**, which cost **network and battery** |
| **Works across devices**, since progress lives on the backend | The **data can be stale or wrong**: a finished episode may still appear, or the position may be off if saving failed |

---

## Next Episode

**Next episode** is what the app **plays or suggests when an episode ends**.

| User finishes                        | Next item          |
| ------------------------------------ | ------------------ |
| **S1E3** (a normal episode)          | S1E4               |
| **Last episode of a season**         | S2E1               |
| **Last episode of the series**       | **No next item**   |

> Usually the **backend decides** this, but the **app has to handle all three cases**.

| ✅ Pros | ❌ Cons |
| ------- | ------- |
| Supports **binge watching** with no extra taps | Has **edge cases**: the last episode of a season, the last episode of a series, **specials**, and episodes **blocked in the user's country** |

---

## Pagination

**Pagination** means **loading a long list in pieces** instead of all at once.

```
Load page 1 → user scrolls near the end → load page 2 → ... → hasMore = false (stop)
```

| ✅ Pros | ❌ Cons |
| ------- | ------- |
| **Faster first load** | Classic bugs (see below) |
| **Less memory** | **On TV**, focus can **get stuck at the end of the list** while a new page loads |
| **Less data transferred** | |

### Classic Pagination Bugs

| Bug                        | Cause                                              |
| -------------------------- | -------------------------------------------------- |
| **Duplicate items**        | Data changes between pages                         |
| **Double fetch**           | Fast scrolling                                     |
| **A list that never ends** | `hasMore` was never set to `false`                 |
