# Handoff brief — ComfyUI capsule-graphic generation (for the MCP-connected Claude)

You are picking up one slice of a larger project: generating the print-ready illustrated
graphics for **Seagrape Supply Co.'s** Admirals Cove capsule via ComfyUI / Comfy Cloud.
Everything you need is in this repo; this brief is self-contained. **Read `PROJECT_BRIEF.md` at
the repo root too** — it's the fuller project memory (brand, business model, all five drops'
full generation prompts).

## Repo & assets
- **Repo:** `benweiner14-source/seagrape`  **Branch:** `claude/seagrape-repo-setup-gfmnyb`
- Clone/pull that branch first — it contains the drop prompts and (once Ben adds them) his
  on-the-water reference photos:
  - `capsules/admirals-cove/refs/` — Ben's real reference photos (channel markers 49/52,
    Manatee Zone sign, the actual burgee flag) — **not yet added to the repo, see below**
  - `docs/comfy-cloud-catalog.md` — **read this first**: what's in the Comfy Cloud model
    catalog, what's been tried, what failed, and why (fill this in as you go — it's currently a
    template, this project hasn't run a single Comfy generation yet)
  - `docs/comfyui-workflow.md` — the node-graph plan (style + composition, two paths)
  - `docs/comfy-cloud-loras.md` — candidate style LoRAs to search for / upload
  - `PROJECT_BRIEF.md` — every drop's full generation prompt, locked colors, blank/placement

## ⚠️ Reference photos aren't in the repo yet
`PROJECT_BRIEF.md` describes photos Ben took on the water (channel marker 52, channel marker 49,
the Manatee Zone sign, a close-up of it, and the actual Admirals Cove burgee) but they haven't
been committed to this repo — this web session doesn't have image upload access. Before running
the photo-referenced drops (1, 4, 5) properly, get those files into
`capsules/admirals-cove/refs/` (ask Ben to drop them in, or upload via Comfy Cloud's
`upload_file` tool directly if you just need them in-session). Drop 3 (burgee) and the logo can
proceed from text description alone since their geometry is simple and fully specified in the
prompt.

## The goal
Generate each of the five drops (see `PROJECT_BRIEF.md` for full prompts) as a **print-ready,
flat-color vintage illustration** — loose woodcut / botanical-field-guide linework, confident and
slightly worn, screen-print-safe (each drop has a locked 2–4 color palette tied to a specific
Comfort Colors 1717 blank). Output needs a transparent background so it can go straight into the
Printful mockup generator.

## Status per drop (don't re-generate what's already approved)
| Drop | Name | Status | Notes |
|---|---|---|---|
| 1 | The Inlet (lighthouse from water) | Not generated to satisfaction | Needs the water-level, off-center composition — see hard constraint below |
| 2 | The MacArthur (editorial still life) | ✅ **Generated & approved via Higgsfield** — treat as the style bar to match, don't re-run | Center chest, cream blank |
| 3 | The Burgee (flag typography) | Prompt approved in concept, not yet generated | No photo reference needed — geometry is in the text |
| 4 | Manatee Zone (speed sign) | Not yet generated | Best starter drop — clearest photo reference, see `comfyui/` starter workflow |
| 5 | Red Right Returning (channel markers) | Not yet generated | Two markers, two colors, symmetrical-but-not composition |

## Hard constraints (do not violate)
- **Style must stay flat illustration, not photoreal and not glossy digital art.** This project's
  entire differentiator is the "old Florida trading post, 1940s–70s field guide" feel — a
  polished/gradient AI-art look or a photoreal render are both misses, just in different
  directions. See `docs/comfyui-workflow.md`'s dials section.
- **Locked color counts per drop** — each drop's prompt in `PROJECT_BRIEF.md` states an exact
  color list (e.g. Drop 1: deep teal background + cream illustration + brick red on the tower
  only). Do not let the model add incidental colors — it has to actually screen print.
- **Composition for Drop 1 specifically:** must NOT be a symmetrical lighthouse flanked by two
  palms (that reads as a gift-shop tee — this was explicitly rejected already). The lighthouse
  must emerge from a treeline, seen from water level, off-center. This is the one drop with a
  documented prior rejection — don't repeat it.
- **Club name / date text** must stay legible where the prompt calls for it (e.g. "ADMIRALS COVE
  — JUPITER INLET", "EST. 1987") but don't fight garbled text in-generation — see the dial for
  this in `docs/comfyui-workflow.md`.
- **No literal placeholder/city text baked into art that isn't meant to be legible** — if a prompt
  edit ever introduces an invented place name for flavor, strip it before it reaches the model
  (LonnieAI hit this exact bug: any proper-noun-shaped phrase in the prompt text risks rendering
  as literal on-canvas text, wanted or not).

## What's already been tried
Nothing yet on Comfy — this is a fresh pipeline. Drop 2 was generated and approved via
**Higgsfield GPT Image 2** directly (not Comfy), and is the one existing reference for "did this
nail the brand's style." Everything else in `PROJECT_BRIEF.md`'s "What's Left To Do" list is
pending.

## Current recommended path — try this first
**Path A from `docs/comfyui-workflow.md`**: Comfy Cloud's partner node (`partner_generate`,
provider `google/nano-banana-pro` or `openai/gpt-image-2`) with the drop's prompt as-is — no
LoRA/ControlNet setup needed. Start with **Drop 4 (Manatee Zone)** — it has the clearest
composition reference once Ben's photo is in `capsules/admirals-cove/refs/`, and there's a
starter Comfy workflow already wired to it in `comfyui/` if Path A underperforms and you need
Path B's real ControlNet control.

## Tuning
- Too photoreal / too glossy → see the dials table in `docs/comfyui-workflow.md`.
- Wrong composition (photo-referenced drops) → raise the reference image's role-tag strength
  (Path A) or ControlNet weight (Path B).
- Colors drifting off the locked palette → this is a **hard-rule failure** for a screen-printed
  product, not just quality — restate the exact color list at the end of the prompt and re-test
  before batching.

## Definition of done
A transparent-background, print-ready illustration that reads clearly as the same locked
vintage-woodcut style as the approved Drop 2, matches the drop's locked color palette exactly,
and — for Drops 1/4/5 — recognizably holds the real composition from Ben's reference photo. Save
outputs, run them through the Printful mockup generator to sanity-check on the actual blank, and
report back which settings worked so the recipe can be locked and repeated across the remaining
drops (and later, other clubs).
