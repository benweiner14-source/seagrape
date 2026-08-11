# Reference photos — Admirals Cove

Ben's real on-the-water photos go here. Used to:
1. Hold composition in ComfyUI img2img/ControlNet (see `docs/comfyui-workflow.md`).
2. Attach as a role-tagged reference image if generating via a Comfy partner node (Nano Banana
   Pro / GPT Image 2) instead — role-tag it as "composition/subject reference only, not for
   photoreal style" (same technique LonnieAI documents in its `docs/multi-image-role-tagging.md`,
   worth porting here if this project ends up needing more than one reference image per drop).

**Not yet added — these need to come from Ben:**
- `manatee-zone-sign.jpg` — the sign on two weathered pilings, wide shot (Drop 4)
- `manatee-zone-sign-closeup.jpg` — close-up: white sign, orange border, red circle, no slash (Drop 4)
- `admirals-cove-burgee.jpg` — the actual club burgee flag: navy pennant, copper/bronze circle,
  vertical pole (Drop 3, now the universal left-chest logo — optional, the flag's geometry is
  already fully specified in the prompt text, but a real reference photo would tighten
  color/proportion accuracy, especially useful for the small-scale chest resize this needs)

**No longer needed:** `channel-marker-52.jpg` and `channel-marker-49.jpg` were for Drop 5 (Red
Right Returning), which is nixed — cut from the capsule entirely.

Commit these normally (not gitignored) — the same way LonnieAI's `creators/*/refs/` photos are
committed, since local Claude Code (and this web session) both need to be able to read them.
