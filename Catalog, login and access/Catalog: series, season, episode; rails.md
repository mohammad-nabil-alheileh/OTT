# Catalog: Series, Season, Episode; Rails

## The Catalog Hierarchy

The **catalog** is **all the content the app can show**. It is organized in a **hierarchy**:

```
Series  ("Breaking Bad")
 └─ Season
     └─ Episode  ← has the video
```

| Level       | What it is                                                     |
| ----------- | -------------------------------------------------------------- |
| **Series**  | The **show itself**                                            |
| **Season**  | A **group of episodes** inside a series                        |
| **Episode** | The **thing you actually play**, and it has a **video**        |

## Rails

A **rail** is **one horizontal row of tiles** on a screen, with a **title above it**, such as "Trending now" or "New episodes".

> The **Home screen** is a **vertical stack of rails**.

```
Home
 ├─ Rail: "Trending"          → [tile][tile][tile][tile] →
 ├─ Rail: "Comedy series"     → [tile][tile][tile][tile] →
 └─ Rail: "Continue Watching" → [tile][tile][tile] →
```

---

## Pros and Cons

### Series → Season → Episode

| ✅ Pros                                                                                   | ❌ Cons                                                                                                                         |
| ---------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| **Matches how viewers think**, and makes "next episode" and a season picker natural to build | **Adds nesting**, so you may need **several requests** to reach one episode                                               |
| **Each level can load separately**, so you don't fetch 200 episodes to show a poster     | Has **edge cases** (see below)                                                                                                  |

#### Edge Cases

- A series with **one season**
- **"Specials"** seasons
- Episode numbers that **restart each season**
- **Movies** that don't fit the hierarchy

### Rails

| ✅ Pros                                                                              | ❌ Cons                                                                                                    |
| ----------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| Users **know the pattern** from every streaming app, and it **scales** to any number of categories | **Lists nested inside lists** are heavy on **performance and memory**, especially with many images on weak TV hardware |
| The **backend can add, remove, or reorder rails** without an app release            | **Focus handling is harder on TV**, because the remote has to move sensibly between rails and tiles       |
