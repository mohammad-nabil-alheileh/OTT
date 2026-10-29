# Crash Reporting

**Crash reporting** automatically **captures what went wrong** when the app breaks and **sends it to a server**, so you see the problem **without the user having to describe it**.

---

## Kinds of Crashes in React Native

React Native has **two worlds**, **JavaScript** and **native**, and **both can fail**.

| Kind                                 | World       | What it is                                                                                                                       |
| ------------------------------------ | ----------- | -------------------------------------------------------------------------------------------------------------------------------- |
| **JS exceptions**                    | JavaScript  | A bug in your React code, such as `undefined.map`. **Fatal** ones close the app in release builds, and **non-fatal** ones are caught and logged |
| **Unhandled promise rejections**     | JavaScript  | An `await` that fails with **no `catch`**                                                                                        |
| **Native crashes**                   | Native      | In **Java/Kotlin** on Android, **Swift/Obj-C** on iOS and tvOS, or **C++** inside libraries like the video player              |
| **ANR** (Android Not Responding)     | Native      | The **main thread is blocked for about 5 seconds**, so Android offers to kill the app. This also applies to **Android TV**      |
| **Out-of-memory (OOM) kills**        | OS          | The OS kills the app because it **used too much memory**                                                                        |

> **OOM kills are especially common on TV.** TVs have **far less RAM than phones**, and TV apps use video and large images. There is **often no error message at all**, so reporters **detect it indirectly**.

## What a Crash Report Contains

| Field               |
| ------------------- |
| **Stack trace**     |
| **Device model**    |
| **OS version**      |
| **App version**     |
| **Memory state**    |
| **Last breadcrumbs** |

---

## Symbolication

Release builds are **minified**, so a raw stack trace looks like this:

```
a.b.c is not a function at index.bundle:1:48213
```

To read it, the tool needs the **matching mapping file uploaded for that exact build**:

| Platform          | Mapping file               |
| ----------------- | -------------------------- |
| **JS**            | Source maps                |
| **iOS and tvOS**  | dSYM files                 |
| **Android**       | ProGuard/R8 mapping files  |

> If these are **missing**, you get **unreadable traces**. If you see **"unsymbolicated"** in a report, the usual cause is that the **mapping upload failed in the build pipeline**.
