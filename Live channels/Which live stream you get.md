# Which Live Stream You Get

The **same channel** can have **different streams for different regions**.

| User's region     | Stream they get     |
| ----------------- | ------------------- |
| **US**            | US stream           |
| **Canada**        | Canada stream       |
| **Everyone else** | Global stream       |

> The **channel name is the same**, but the video behind it can differ in **ads, schedule, or even content**, because of **licensing and regional rights**.

## Things to Keep in Mind

| Topic                              | Detail                                                                                                                         |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| **Don't hardcode the stream**      | Ask the backend each time, so rules can change **without a release**                                                          |
| **Always have a default**          | An unknown or missing country must **fall back to Global**, not break                                                         |
| **Testing is harder**              | You see only your own region, so a bug may exist only for US or Canada users. A **VPN or a backend override** helps reproduce it |
| **Schedules may differ per region** | "Now" in the US stream may not match "Now" in the Global stream                                                              |
