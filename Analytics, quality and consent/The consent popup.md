# The Consent Popup

**Didomi** is a **CMP (Consent Management Platform)**. It does **three jobs**:

| # | Job                                                                                  |
| - | ------------------------------------------------------------------------------------ |
| 1 | **Shows the popup** in the right **language** and for the right **region**           |
| 2 | **Stores the user's choices** and **keeps proof** of them                            |
| 3 | **Tells your app what each user allowed**, so your code can switch tools on or off   |

> **The popup is not the enforcement. Your code is.** If the app ignores Didomi's answer, the popup is just decoration and you are **still breaking the law**.

```
Didomi popup → user's choices → your gated tracking layer → each tool ON / OFF
```

---

## The Five Switches

Your app has **five things** the popup can turn on or off:

| Switch                   | What it does                                                | Why it needs consent                                          |
| ------------------------ | ----------------------------------------------------------- | ------------------------------------------------------------- |
| **Google Analytics**     | General app usage: screens, taps, sessions                  | Tracks behaviour with device or user identifiers              |
| **Parse.ly**             | Content analytics: which articles and videos are popular    | Tracks what each viewer reads and watches                     |
| **Youbora**              | Video quality and playback analytics                        | Sends playback events tied to a device or user                |
| **Feature-flag logging** | Records which variant of an experiment a user saw           | Usually tied to a user or device ID                           |
| **Personalised ads**     | Ads targeted using viewing behaviour                        | Targeted advertising is the **most strictly regulated** purpose |

---

## Key Points to Remember

| Point                               | Detail                                                                                                 |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------ |
| **Who does what**                   | Didomi **collects and stores** the choice. **Your code enforces it**                                   |
| **Five switches**                   | Google Analytics, Parse.ly, Youbora, feature-flag logging, personalised ads                            |
| **One gated layer**                 | Route **every tracking call** through one gated layer, and **re-apply it when consent changes**        |
| **Consent can change later**        | **Listen for changes**, not only the launch state                                                      |
| **The popup loads asynchronously**  | **Early events** need a clear rule                                                                     |
| **TV**                              | The popup **must work with a remote**                                                                  |
