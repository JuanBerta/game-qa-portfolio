---
AIGC:
    Label: "1"
    ContentProducer: 001191440300708461136T1XGW3
    ProduceID: 89238829fb97168b9c4195c03c152aef_74cb4852bf6211f197eb525400393706
    ReservedCode1: uUbYKwz/NmwvvjjzXcf6pPH83LiebcvclaKZ4Jky0ntJnrzbhg2PKFjcnhbDBAF4OWcQJxBsPPuwBL0X7eWLb0NTV0rsdQIPu6IBe2I58u7+OaiHrsZsi8X7T4u983hc9b4Rqn1CmFxTl1AZ26mAjoT1qT3Nu8rHbZgvVAHC0O8B+W3JlkLFSOsTL4w=
    ContentPropagator: 001191440300708461136T1XGW3
    PropagateID: 89238829fb97168b9c4195c03c152aef_74cb4852bf6211f197eb525400393706
    ReservedCode2: uUbYKwz/NmwvvjjzXcf6pPH83LiebcvclaKZ4Jky0ntJnrzbhg2PKFjcnhbDBAF4OWcQJxBsPPuwBL0X7eWLb0NTV0rsdQIPu6IBe2I58u7+OaiHrsZsi8X7T4u983hc9b4Rqn1CmFxTl1AZ26mAjoT1qT3Nu8rHbZgvVAHC0O8B+W3JlkLFSOsTL4w=
---



# BUG-027: Gathering, Crafting, and Other Action Audio Cues Intermittently Stop Working; Restart Does Not Always Restore Them

## Problem Description
During normal gameplay, gathering, crafting, and other action-based sound cues sometimes stop playing entirely and without warning. The audio loss is intermittent: the same activity may produce sound in one session and remain silent in another, with no obvious trigger (no disconnect, no settings change, no UI state change observed).

Restarting the game client **sometimes** resolves the issue but **not always** — on certain occasions the sound cues remain missing even after a full restart. This behavior differs from a pure in-session audio desync (see BUG-023) because the failure can persist across client restarts, suggesting the cause is not solely tied to the network reconnection flow.

---

## Steps to Reproduce
1. Launch the game and confirm that gathering/crafting sound effects play normally.
2. Play for an arbitrary period; at some point, note that gathering, crafting, and other action audio cues stop playing (no error message, no settings change).
3. Attempt to continue the same activity — the cues remain silent for the rest of the affected period.
4. Restart the game client.
5. Observe that the audio cues are sometimes restored after restart, but on other occasions remain missing even after the restart.

---

## Expected vs. Actual Result

| Type | Result |
| :--- | :--- |
| **Expected Result** | Action-based audio cues (gathering, crafting, other feedback sounds) should play consistently throughout a session, and a full client restart should always restore the audio engine to a working state. |
| **Actual Result** | Action audio cues intermittently stop working; restarting the game sometimes fixes the issue but does not always, leaving the affected sounds silent indefinitely. |

---

## Technical Observations & Potential Causes
* **Audio Engine Channel / Instance Exhaustion:** Prolonged sessions with repeated gathering/crafting actions may exhaust finite audio instances or voice channels inside the client audio engine; when the limit is reached, new action cues silently fail to spawn rather than erroring out.
* **Event Listener State Loss Not Tied to Reconnection:** Unlike BUG-023 (which follows a disconnect/reconnect event), this audio loss can appear without any network transition, implying a separate listener or audio bank state that can be invalidated by routine gameplay flow.
* **Persistent Audio State Across Restarts:** Because the issue can survive a full restart, a non-reset state (e.g., cached audio configuration, persisted bus settings, or session-scoped audio flags written back to disk) may keep the affected cues disabled even after the client is relaunched.
* **Race Condition on Audio Bank Loading:** On some launches, the audio bank responsible for action cues may fail to fully initialize (or initialize out of order), leaving those cues absent until the bank is reloaded by an unrelated event.

## Screenshot

No screenshot available — the issue is audio-only and manifests over time.
*（内容由AI生成，仅供参考）*
