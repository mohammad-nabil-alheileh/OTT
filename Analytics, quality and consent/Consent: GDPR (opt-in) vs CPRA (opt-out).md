# Consent: GDPR (Opt-In) vs CPRA (Opt-Out)

Consent rules decide **when the user's permission is needed**.

## The Two Approaches

### GDPR: Opt-In

**GDPR** (EU/EEA, plus the UK's version) is **opt-in**. For **non-essential tracking**, you must have the user's **consent before you collect anything**.

> **No answer means no.**

### CPRA: Opt-Out

**CPRA** (California, an update of the CCPA) is **opt-out**. You **may collect by default**, as long as you **tell the user**. They can then **say stop**, mainly for the **"sale" or "sharing"** of their data.

```
GDPR (opt-in):   collection OFF ── user agrees ──▶ collection ON
CPRA (opt-out):  collection ON  ── user refuses ─▶ collection OFF
```

## Comparison

| Aspect                              | GDPR (opt-in)                                                                    | CPRA (opt-out)                                                                   |
| ----------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| **Region**                          | EU/EEA, plus the UK's version                                                    | California (an update of the CCPA)                                               |
| **Default before the user answers** | ❌ **Off**, nothing non-essential collected                                      | ✅ **On**, collection allowed with notice                                        |
| **What the user must do**           | **Actively agree**                                                               | **Actively refuse**                                                              |
| **Main focus**                      | **All personal data processing**, including cookies and device IDs               | **Sale or sharing** of data, targeted ads, sensitive data                       |
| **Consent quality**                 | Must be **specific, informed, unambiguous**, and **as easy to withdraw as to give** | Must offer a **clear opt-out**, such as a **"Do Not Sell or Share My Personal Information"** link |

---

## Essential vs Non-Essential

Under opt-in rules, **"no consent" does not mean "no data at all"**.

| Data type                                       | Needs consent? |
| ----------------------------------------------- | -------------- |
| **Strictly necessary** to run the service       | ❌ No          |
| **Analytics**                                   | ✅ Yes         |
| **Personalisation**                             | ✅ Yes         |
| **Advertising**                                 | ✅ Yes         |

> **Which category each tool falls into**, such as **crash reporting**, is a **decision your company makes**, not one the code can make.
