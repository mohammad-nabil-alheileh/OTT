# Authentication vs Entitlement

| Check              | Question it answers                                                                 | Answered by / depends on                  |
| ------------------ | ----------------------------------------------------------------------------------- | ----------------------------------------- |
| **Authentication** | **Who are you?** Are you really this user?                                          | **Login and tokens**                      |
| **Entitlement**    | **What are you allowed to watch?** Does this user have the right to play this specific video? | **Plan, purchase, region, or rights** |

```
Request to play a video
   │
   ├─ 1. Authentication: who are you?        ── fail → sign in
   │
   └─ 2. Entitlement: can you watch this?    ── fail → not allowed
          │
          └─ pass → play
```

> You can **pass the first and fail the second**. **Being logged in does not mean you can play everything.**
