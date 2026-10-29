# 3 Live Channels (BTV, BTV+, Originals)

## The Schedule

Every live channel airs a **sequence of programs**, like a TV guide. The schedule answers **three questions**:

| Question          | Answer                                                        |
| ----------------- | ------------------------------------------------------------- |
| **Now**           | What is airing at this moment                                 |
| **Next**          | What airs right after it                                      |
| **Full Schedule** | The whole list of programs for the channel, usually by day    |

## How "Now" Is Decided

Each program has a **start time** and an **end time**. The app decides which program is **"Now"** by comparing the **current time** with those times.

```
start ≤ current time < end  →  this program is "Now"
```

## In a Real App

Times are **full timestamps** (UTC from the backend), not minutes, and the **"now" value comes from a clock that refreshes**.

### Two Things to Keep in Mind

| Topic                   | Detail                                                                                                                                       |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| **Time must be re-checked** | If the screen stays open, Now and Next must **update when a program ends**, usually with a **timer set for the end time** of the current program |
| **Time zones**          | **Store and compare in UTC**, and only format in the user's **local time for display**                                                       |
