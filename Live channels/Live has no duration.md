# Live Has No Duration

An **on-demand video** has a **known length**, like `6120` seconds. A **live stream has no end**, so it has **no length**.

The player reports **`-1`** as the duration: a placeholder meaning **"unknown / not applicable"**.

| Video type    | Duration reported | Meaning                  |
| ------------- | ----------------- | ------------------------ |
| **VOD**       | e.g. `6120`       | Known length in seconds  |
| **Live**      | `-1`              | Unknown / not applicable |

## Why Live Is Left Out of Continue Watching

**Continue Watching** is the row that lets users **resume what they started**. It works by saving the **position** and the **duration** of a video, so the app can show a **progress bar** and **resume at the right spot**.

| Needed for Continue Watching | VOD    | Live                                          |
| ---------------------------- | ------ | --------------------------------------------- |
| **Duration**                 | ✅ Yes | ❌ No                                         |
| **Position to resume**       | ✅ Yes | ❌ No, you always rejoin at the live point    |

> So **live is left out** of the Continue Watching row.

## Things to Keep in Mind

### `-1` Is a Sentinel Value

A **sentinel value** is a special number meaning **"no value"**. **Never use it in calculations.**

### Check `duration > 0`, Not Just `!== -1`

That way **`0`, `NaN` or `undefined`** are also handled.

```js
// ❌ Misses 0, NaN, undefined
if (duration !== -1) { ... }

// ✅ Handles all of them
if (duration > 0) { ... }
```

### Other Places That Use Duration Have the Same Risk

- The **seekbar**
- The **time label** (`12:30 / 1:42:00`)
- Any **"time left"** text
