# Handoff brief — ComfyUI capsule-graphic generation (for the MCP-connected Claude)

You are picking up one slice of a larger project: generating the print-ready illustrated
graphics for **Seagrape Supply Co.'s** Admirals Cove capsule via ComfyUI / Comfy Cloud.
Everything you need is in this repo; this brief is self-contained. **Read `PROJECT_BRIEF.md` at
the repo root too** — it's the fuller project memory (brand, business model, full generation
prompts for all three shirts + the universal chest logo).

**⚠️ Capsule structure changed since this doc was first written — read `PROJECT_BRIEF.md`'s
"Construction decision" note under "The Capsule" header before doing anything else.** It's now
**4 shirts**: 3 statement back designs (Drops 1, 2, 4, each also carrying a small left-chest
burgee) + Drop 3 as its own 4th "essentials" tee (chest burgee only, no back graphic). Drop 5
(channel markers) is nixed entirely. There's also a 12-shot lifestyle "Lookbook Scene Map" now —
see `PROJECT_BRIEF.md` — that's a separate generation task from the 4 print graphics this doc
focuses on, but uses the same Comfy pipeline.

**⚠️ Higgsfield is nixed, Comfy Cloud is now the confirmed pipeline (Ben, latest) — for graphics
*and* lifestyle photography.** Every "generated via Higgsfield" note below describes how the
existing 4 designs got made *before* this switch, not the path forward. Don't read those as a
reason to second-guess standing up Comfy — it's decided, Ben has it set up.

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
`PROJECT_BRIEF.md` describes photos Ben took on the water (the Manatee Zone sign, a close-up of
it, and the actual Admirals Cove burgee) but they haven't been committed to this repo. Before
regenerating Drop 4 or the small-scale Drop 3 chest logo, get those files into
`capsules/admirals-cove/refs/` (ask Ben to drop them in, or upload via Comfy Cloud's
`upload_file` tool directly if you just need them in-session). The channel-marker photos listed
in that folder's README were for the now-nixed Drop 5 and are no longer needed for this capsule.

## The goal
Generate the capsule's **3 back designs + 1 universal chest logo** (see `PROJECT_BRIEF.md` for
full prompts) as **print-ready, flat-color vintage illustration** — loose woodcut /
botanical-field-guide linework, confident and slightly worn, screen-print-safe (each has a locked
2–4 color palette tied to a specific Comfort Colors 1717 blank). Output needs a transparent
background so it can go straight into the Printful mockup generator.

## Status per design (don't re-generate what's already approved)
| Design | Placement | Status | Notes |
|---|---|---|---|
| 1 — The Inlet (lighthouse from water) | Back | ✅ Generated via Higgsfield, pending Ben's final approval — `capsules/admirals-cove/drops/drop-1-the-inlet.png` | Nails the off-center, water-level composition. Still needs the transparent-background export pass (teal fill = shirt color) |
| 2 — The MacArthur (editorial still life) | Back | ✅ **Generated & approved via Higgsfield** — treat as the style bar to match, don't re-run — `capsules/admirals-cove/drops/drop-2-the-macarthur.png` | Still needs the transparent-background export pass |
| 3 — The Burgee | **Small, left chest — universal across all 3 shirts** | ✅ Generated via Higgsfield, already transparent — `capsules/admirals-cove/drops/drop-3-the-burgee.png` | Sized/detailed for a back graphic (full "ADMIRALS COVE — JUPITER FL — EST. 1987" typographic pennant), not a small chest mark — **needs a simplified small-scale regeneration** before use, see `PROJECT_BRIEF.md`'s Drop 3 section |
| 4 — Manatee Zone (speed sign) | Back | ✅ Generated via Higgsfield, pending Ben's final approval — `capsules/admirals-cove/drops/drop-4-manatee-zone.png` | Still needs the transparent-background export pass (cream fill = shirt color) |
| ~~5 — Red Right Returning~~ | — | ❌ **Nixed, cut from the capsule** | No longer part of this project |

**Note:** Designs 1, 3, and 4 above were generated via **Higgsfield directly**, not yet through
Comfy — same as Drop 2. Comfy Cloud is unused for this project's actual output *so far*, but is
now the confirmed pipeline for everything going forward (see the Higgsfield-nixed note above) —
`docs/comfy-cloud-catalog.md` is still a template and should get filled in as the first real
Comfy session runs.

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
provider `google/nano-banana-pro` or `openai/gpt-image-2`) with the relevant prompt as-is — no
LoRA/ControlNet setup needed. The one open generation task is the **Drop 3 small-scale chest
logo** — start there (it's pure text/geometry, no photo reference needed). If Ben wants any of
Drops 1/2/4 regenerated too, there's a starter Comfy workflow in `comfyui/` (currently wired to
the Manatee Zone prompt) for Path B's real ControlNet control if Path A underperforms.

## Tuning
- Too photoreal / too glossy → see the dials table in `docs/comfyui-workflow.md`.
- Wrong composition (photo-referenced drops) → raise the reference image's role-tag strength
  (Path A) or ControlNet weight (Path B).
- Colors drifting off the locked palette → this is a **hard-rule failure** for a screen-printed
  product, not just quality — restate the exact color list at the end of the prompt and re-test
  before batching.

## Definition of done
A transparent-background, print-ready illustration that reads clearly as the same locked
vintage-woodcut style as the approved Drop 2, matches the design's locked color palette exactly,
and — for Drop 4 specifically — recognizably holds the real composition from Ben's reference
photo. Save outputs, run them through the Printful mockup generator to sanity-check on the actual
blank, and report back which settings worked so the recipe can be locked and repeated (and later,
applied to other clubs).
