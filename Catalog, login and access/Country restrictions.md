# Country Restrictions

Content owners often **sell the rights to a video country by country**. So each **on-demand video (VOD)** carries a **country rule**, and the **backend checks it before allowing playback**.

## Two Ways to Express the Rule

| Rule type      | Meaning                                                  | Example (`JO`, `EG`)                  |
| -------------- | -------------------------------------------------------- | ------------------------------------- |
| **Allow list** | The video can play **only in these countries**           | Plays in Jordan and Egypt only        |
| **Block list** | The video can play **everywhere except these countries** | Plays everywhere except Jordan and Egypt |

## Country Codes

Country codes are usually the **two-letter ISO codes**:

| Code   | Country       |
| ------ | ------------- |
| `JO`   | Jordan        |
| `EG`   | Egypt         |
| `US`   | United States |

## Rules Are per Video

> Rules are **per video**, not per series or rail.

- **Two videos in the same series** can have different rules.
- **One tile in a rail may play** while its **neighbor is blocked**.
