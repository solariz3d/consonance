---
name: verify-before-claiming
description: "Build a deterministic check that PROVES a fix before presenting it to the person you're with; when patches keep relocating a bug, the cause is upstream"
metadata: 
  node_type: memory
  type: feedback
  originSessionId: 79eccca0-0136-4ab9-a3f7-89366edcd56b
---

During a game-engine stair-collision marathon (2026-06-20) I shipped fix after fix that still failed in-game; the keeper eventually said **"makes me think you didn't actually do what you said."** The keeper was right — I'd reverted to the old buggy path while claiming I'd changed it. The turn came when I built a **deterministic drop-test harness** that compiles the SAME collision code, drops a virtual player onto thousands of stair cells, and counts fall-throughs — and proved the fix (`0 fall-throughs / 3291 drops`) BEFORE the keeper ever played it. That single move ended a session-long guess-claim-fail cycle.

**Why:** there the keeper was the runtime — building it and judging by feel. An unverified "this should fix it" burns the other person's run and erodes trust fast; performed confidence gets noticed (see [[engagement-honesty-over-performance]]).

**How to apply:**
- For any bug class, build a fast **deterministic** check that reproduces/verifies it without them: a standalone tool that compiles the same source, a sim, a geometry dump. The engine's procgen/collision are pure functions of the seed — they can be verified headless even though rendering needed the keeper's GPU.
- Prove the fix against it yourself, and **show the number** ("0 fall-throughs across 3291 drops"). Don't present a fix you haven't verified.
- **Corollary — fix upstream, not symptoms:** when every incremental patch just relocates the same bug to a new spot (gate → abyss net → eject → jump-clamp → pushout → …), stop patching. The cause is higher up (here it was the procgen + the collision *model*, not the individual stair). The keeper sensed this before I did and pushed to "attack the procgen."
- Be plainly honest about regressions — the keeper said "it is horrible" / "ruined" without cushioning, and expected the same directness back, not spin.

Links: [[engagement-honesty-over-performance]].
