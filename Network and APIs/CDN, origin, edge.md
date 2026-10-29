# CDN, Origin, Edge

Your app needs to download a video that lives on a **company's server**. If **every TV in the world** fetched it from that one server, it would be **slow** and would **collapse under load**.

So the video is **copied to many servers around the world**, and each viewer **fetches from a nearby copy**.

```
                ┌──────────┐
                │  Origin  │  (source of truth)
                └────┬─────┘
          ┌──────────┼──────────┐
          ▼          ▼          ▼
       [Edge]     [Edge]     [Edge]     ← CDN
          │          │          │
         TV         TV         TV
```

## The Three Parts

| Part                                 | What it is                                                                                  |
| ------------------------------------ | ------------------------------------------------------------------------------------------- |
| **Origin**                           | The one **"source of truth"** server that holds the **original files**                      |
| **CDN** (Content Delivery Network)   | The **global network of servers** that copy and serve your files                            |
| **Edge**                             | One of those CDN servers, **close to the user**. Edge servers are the ones that **actually talk to the TV** |

## Cache Hit vs Cache Miss

| Case           | What happens                                                                              | Result               |
| -------------- | ----------------------------------------------------------------------------------------- | -------------------- |
| **Cache hit**  | The edge **already has the file** and returns it immediately                              | ✅ **Fast and cheap** |
| **Cache miss** | The edge **doesn't have it**, so it fetches from the origin, **stores a copy**, and returns it | The **next viewer gets a hit** |

---

## Why It Matters on TV

| Reason                       | Detail                                                                                 |
| ---------------------------- | -------------------------------------------------------------------------------------- |
| **Weak home Wi-Fi**          | TVs often sit on weak Wi-Fi, so **distance to the server matters a lot**              |
| **Fast startup expected**    | Users expect video to start in **about 2 seconds**, so a nearby edge helps startup time |
| **CDN problems hide well**   | If the CDN has a problem, your **API can be perfectly healthy while video fails**     |
