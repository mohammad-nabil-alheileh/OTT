# Weak Decoders on Samsung and LG

## What a Decoder Does

Video files are **heavily compressed**. A **decoder** turns the compressed data back into pictures.

On TVs this is usually a **dedicated hardware chip**, because doing it in software would be far too slow.

> **Shaka only moves the bytes.** The TV's decoder does the heavy lifting, so **the decoder sets the limits**, whatever Shaka does.

---

## Why TV Decoders Are "Weak"

TVs are **built to a price**, and the chip and the browser engine that runs our web app are often **several years old**, even on a new TV.

### Typical Limits

| Limit                                  | What it means                                                                                                       |
| -------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| **Limited resolution and bitrate**     | The top rung of the ladder may be more than the chip can decode smoothly                                           |
| **Limited codec support**              | Older TVs may not decode newer codecs such as **HEVC** or **AV1**, or only decode them at certain profiles and levels |
| **Few simultaneous decoders**          | Some TVs can only run **one video decoder at a time**, so a preview video plus a main video can fail               |
| **Little memory and a slow CPU**       | The JavaScript side shares those resources with decoding                                                           |
| **Strict MSE implementation**          | The TV's browser may be picky about how segments are appended, so streams that work in Chrome can stall on TV      |

---

## Symptoms

- **Choppy or stuttering** video that is smooth on a desktop
- **Frozen frame with audio still playing**, or the reverse
- **Playback stalls** when ABR switches rungs
- **Black screen**, or a decode error with no obvious cause
- **Works on one TV model and fails on another**, even from the same brand

---

## What We Can Do About It

### 1. Cap the Ladder

Don't let ABR choose rungs the TV **can't handle**.

### 2. Tune Buffering

On weak TVs it's a **balance**:

| Buffer goal | Benefit                 |
| ----------- | ----------------------- |
| **Smaller** | Uses less memory        |
| **Larger**  | Survives network dips   |

### 3. Special Settings for Live

Live is the **hardest case** for a weak TV, because the player must keep **re-fetching the playlist** while **decoding** and **staying near the live edge**.

Typical areas to tune:

| Area                          | What to tune                                                                                          |
| ----------------------------- | ----------------------------------------------------------------------------------------------------- |
| **Live edge distance**        | How far behind the live edge to stay                                                                  |
| **Retries and timeouts**      | Behaviour for playlist and segment requests                                                           |
| **Gap handling**              | Live streams can have small holes in the timeline that weak players stall on unless told to skip them |

### 4. Choose Renditions and Codecs the TVs Support

The best fix is often on the **stream side**:

- Offer **H.264** renditions that every TV can decode.
- Don't depend on a codec **only some TVs support**.

### 5. Test on Real Devices

> **Chrome on a laptop** is a great debugging tool but a **poor predictor** of how a TV behaves. A stream that plays perfectly there can still fail on a TV.
