# Keys from Remote Config

The values **Google DAI needs** are **not hardcoded** in the app logic:

- the **asset keys** for live channels
- the **content source ID**
- any **related IDs**

They live in **remote config**: a settings file or service **hosted outside the app**, which the app **downloads at startup**.

> You can **change it without shipping a new app version**.

## The Backup Copy

The app also **ships with a backup copy** of those values inside it. If the remote fetch fails, the app **uses the backup**.

### Where the Values Come From

| Priority | Source                         | When it's used                                   |
| -------- | ------------------------------ | ------------------------------------------------ |
| 1        | **Remote config**              | Fetched at startup, **valid and on time**        |
| 2        | **Cached last good config**    | Remote fetch failed (used by many apps)          |
| 3        | **Bundled backup**             | Nothing better is available                      |

```
Fetch remote config
   ├── OK and valid ───────────────▶ use remote
   └── failed / timed out / invalid
          ├── cached last good? ───▶ use cache
          └── no cache ────────────▶ use bundled backup
```

---

## Three Details That Matter

| Detail         | What to do                                                                                                                      |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| **Timeout**    | Don't make the viewer wait 30 seconds for config. **A few seconds, then fall back**                                            |
| **Validation** | Check that the remote values **exist and have the right shape** before trusting them. A **half-empty remote config is worse than a failed one** |
| **Caching**    | Many apps also keep the **last good remote config** on the device, and use it **before the bundled backup**                    |
