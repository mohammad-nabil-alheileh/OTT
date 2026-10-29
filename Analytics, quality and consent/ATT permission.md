# ATT Permission

**ATT (App Tracking Transparency)** is **Apple's own permission system**, built into **tvOS** (and iOS). Before an app may track the user, the **operating system must show a system dialog** and the **user must allow it**.

## What Counts as "Tracking"

In Apple's definition, **tracking** means:

- **linking data** from your app with data from **other companies' apps or websites** for **targeted advertising** or **ad measurement**, or
- **sharing it with data brokers**.

> **Ordinary first-party analytics** that stay inside your own app are **generally not "tracking"** under this definition. But whether a specific tool counts is a **decision for your team and Apple's rules**, so **check it rather than assume**.

## The IDFA

The practical effect is on the **IDFA (Identifier for Advertisers)**: the **device ID** that advertising systems use to **recognise a device across apps**.

| ATT result       | IDFA                       |
| ---------------- | -------------------------- |
| **Approved**     | ✅ Available               |
| **Not approved** | ❌ Returned as **all zeros** |

---

## Didomi Popup vs ATT Prompt

| Aspect                          | Didomi popup                   | ATT prompt                                          |
| ------------------------------- | ------------------------------ | --------------------------------------------------- |
| **Who owns it**                 | Your company, via the CMP      | Apple, the OS                                       |
| **What it answers**             | Do the **privacy laws** let us? | Does the **platform** let us?                      |
| **Looks like**                  | Your branded popup             | A standard system dialog                            |
| **Can you change the wording?** | ✅ Yes                         | Only **one explanatory line** (the usage description) |
| **Remembered by**               | Didomi                         | The OS, per app                                     |

> A user can say **yes in Didomi and no in ATT**, or the reverse. **The safe rule:** use the personalised path **only when both say yes**.

| Didomi | ATT    | Personalised path? |
| ------ | ------ | ------------------ |
| ✅ Yes | ✅ Yes | ✅ **Yes**         |
| ✅ Yes | ❌ No  | ❌ No              |
| ❌ No  | ✅ Yes | ❌ No              |
| ❌ No  | ❌ No  | ❌ No              |

---

## The Four Statuses

| Status              | Meaning                                                                                              |
| ------------------- | ---------------------------------------------------------------------------------------------------- |
| **`notDetermined`** | The user **hasn't been asked yet**                                                                   |
| **`authorized`**    | The user **allowed tracking**, and the **IDFA is available**                                         |
| **`denied`**        | The user **refused**                                                                                 |
| **`restricted`**    | The **device settings** or a **parental or organisation policy** block tracking, and **you can't even ask** |

---

## Things to Know

| Topic                         | Detail                                                                                                                                                                                                     |
| ----------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **The prompt appears only once** | After the user decides, you **can't show it again**. To change their mind, they must go to the **system Settings**                                                                                      |
| **Timing matters**            | The prompt only shows when the app is **active and in the foreground**. If you call it too early, it may **silently not appear**. Many apps ask **after the Didomi popup is closed**                       |
| **Order of the two dialogs**  | Showing two dialogs in a row is a **UX decision**. Often the **Didomi popup comes first**, and the **ATT prompt follows only if the user accepted personalised ads**. Asking ATT after a "no" in Didomi is pointless, since the answer would not matter |
| **Remote navigation**         | The system dialog is already usable with the **Siri Remote**, but **your own screen shown before it** needs proper focus handling                                                                          |
| **The text counts**           | Apple **reviews the usage description**, and a **vague or misleading sentence** can cause **App Store rejection**                                                                                          |
| **Only Apple TV**             | **Android TV, Samsung and LG** have their own advertising-ID controls, which work differently                                                                                                              |

### Typical Order

```
App launches → Didomi popup
                  ├── personalised ads: NO  → skip ATT → non-personalised path
                  └── personalised ads: YES → ATT prompt
                                                 ├── authorized → personalised path
                                                 └── denied     → non-personalised path
```
