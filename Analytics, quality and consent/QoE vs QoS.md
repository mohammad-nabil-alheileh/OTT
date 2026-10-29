# QoE vs QoS

**QoS (Quality of Service)** is the **technical side**: what the **system, network and player** are doing. It is **measured by machines**.

**QoE (Quality of Experience)** is the **viewer's side**: how good the experience **felt** and what the viewer **did because of it**. It is measured through **behaviour**, or sometimes through **surveys**.

## Comparison

| Aspect              | QoS                                          | QoE                                                    |
| ------------------- | -------------------------------------------- | ------------------------------------------------------ |
| **Question**        | Is the **system** performing well?           | Is the **viewer** happy?                               |
| **Viewpoint**       | Network, server, player                      | The person watching                                    |
| **Measured by**     | Direct measurement                           | Calculated from events, plus behaviour                 |
| **Who uses it**     | Engineers, DevOps                            | Product, support, engineers                            |

### Typical Metrics

| QoS metrics            | QoE metrics                       |
| ---------------------- | --------------------------------- |
| Bitrate                | Startup time felt by the user     |
| Throughput             | Rebuffer ratio                    |
| Latency                | Resolution actually seen          |
| Dropped frames         | Video start failures              |
| Error rate             | Exits before video start          |
| CDN response time      | Watch time                        |
|                        | Abandonment                       |

---

## Why You Need Both

| Case                       | Example                                                                                                                                   |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| **Good QoS, bad QoE**      | The stream is fast and at high bitrate, but the **app takes a long time to load**, or **audio and video drift apart**. The numbers look fine and **viewers still leave** |
| **Bad QoS, fine QoE**      | Bitrate dips for a few seconds on a **quiet scene** and **nobody notices**                                                               |

> **A common workflow:** **QoE tells you *that* something is wrong**, and **QoS tells you *why*.**
