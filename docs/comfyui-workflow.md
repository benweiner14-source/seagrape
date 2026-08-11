# ComfyUI workflow — capsule graphics (style + composition)

**Why this is easier than the LonnieAI pipeline:** LonnieAI needed three independent locks
(identity + style + pose) because it was rendering a *recognizable real person*. Seagrape's
drops are objects and scenes, not faces — there's no identity to hold. That collapses the
problem to two controls:

1. **Style** — push every drop toward the same locked illustration style: loose vintage
   woodcut / 1940s–70s botanical-field-guide-and-boating-manual linework, confident ink lines,
   slightly worn, **flat color only (no gradients, no photoreal shading, no airbrush)** — it has
   to survive as a 2–4 color screen print on a Comfort Colors tee.
2. **Composition** — for designs built from Ben's actual on-the-water photos (Drop 1
   lighthouse-from-water, Drop 4 manatee sign), hold the real composition/perspective from the
   photo rather than letting the model invent a generic angle. For designs with no photo
   reference (the logo, the Drop 3 chest burgee), skip this — plain prompt is enough since the
   geometry is simple and specified in text. *(Drop 5 — channel markers — is nixed, cut from the
   capsule; no longer a target for this pipeline.)*

Tune each drop until it's clearly the same illustration system *and* clearly the right subject.

## Path A — try this first (no LoRA/ControlNet setup)
Comfy Cloud's **partner nodes** (Nano Banana Pro / GPT Image 2, via `partner_generate`) take the
drop prompt as-is, no custom nodes required. This is the fastest way to see whether a strong
prompt alone lands the flat-woodcut look:
- Provider: `google/nano-banana-pro` (or `openai/gpt-image-2`), 9:16 or the print aspect noted
  per drop in `PROJECT_BRIEF.md`.
- For the three photo-referenced drops, attach Ben's reference photo as image 1 and role-tag it:
  *"REFERENCE IMAGE 1: use ONLY for composition/perspective/subject placement — a real photo,
  reproduce the layout but ignore that it's a photograph. Do not render it photoreal."*
- **Known risk (learned on LonnieAI):** partner-node illustration output tends to default to a
  glossy, generic "AI art" look rather than a flat worn woodcut — if that happens, push harder on
  "flat color, no gradient, no soft shading, hand-cut linocut/woodblock texture" in text, or move
  to Path B for real control.
- **Known risk (learned on LonnieAI):** any literal place name or label in the prompt text
  (e.g. "ADMIRALS COVE", "MANATEE ZONE") can render as garbled or duplicated on-canvas text. Keep
  legible-text asks short, bias toward regenerating on a text-accuracy miss rather than fighting
  it with more instruction, and treat hero typography as a separate clean-up pass (Illustrator/
  Photoshop) rather than something the model must get pixel-perfect in one shot.

## Path B — fallback / full control (SDXL, if Path A underperforms)

### Recommended stack
- **Checkpoint:** an SDXL model with an illustrative/print lean, or base SDXL + a style LoRA (see
  `docs/comfy-cloud-loras.md` for candidates — Comfy Cloud's default catalog is photoreal-first,
  same gap LonnieAI hit).
- **Style:** a **woodcut / linocut / vintage travel-poster / screen-print** LoRA. Weight ~0.6–0.9.
  Push flat color in the prompt regardless of LoRA weight — it's doing real work here.
- **Composition (photo-referenced drops only):** **ControlNet Canny or Lineart** from Ben's
  reference photo (Canny holds hard edges — pilings, sign shape, marker geometry — better than
  Depth does for this kind of flat illustration). Weight ~0.5–0.7. Skip entirely for the logo and
  Drop 3 (no photo reference to hold).
- **Sampler:** img2img with **denoise ~0.65–0.8** off the reference photo (high enough to fully
  restyle into linework, low enough to keep the real composition) — or ControlNet + pure txt2img
  if you want a cleaner break from the source photo's colors/lighting.

### Node graph (Path B, sketch)
```
Load Checkpoint ─┐
Load Style LoRA ─┤→ Model ─┐
                 │         ├→ KSampler → VAE Decode → Save
ControlNet Canny ┘         │   (from Ben's reference photo — photo-referenced drops only)
Positive/Negative prompt (style-lock block below)
```

## Prompt (positive) — style-lock block, reuse across every drop
`Loose vintage woodcut illustration, hand-drawn confident ink lines, slightly worn and imperfect,
flat color only, no gradients, no airbrush, no photoreal shading, screen-print-ready linework,
[N]-color palette only: [list the drop's locked colors]`
**Negative:** `photograph, photorealistic, gradient, airbrush, soft shading, glossy digital
illustration, 3D render, watermark, extra/garbled text`

## Dials to turn if it's...
- **Reads as a photo, not an illustration** → raise LoRA weight, raise denoise (Path B) or push
  harder on "flat color / no gradient / woodcut" (Path A).
- **Reads as generic glossy AI art, not vintage/worn** → add "hand-cut linocut texture, imperfect
  ink line, slightly rough edges" — the failure mode isn't photoreal, it's *too clean*.
- **Wrong composition / doesn't match the real spot** → raise ControlNet weight (Path B) or
  strengthen the composition role-tag on the reference image (Path A).
- **Colors bleeding past the locked palette** → lower CFG slightly, restate the exact color list
  and "N colors maximum" at the end of the prompt, not just the start.
- **Club name / date text garbled** → don't fight it in-generation; regenerate a couple of seeds,
  or drop the typography from the AI pass and set it clean in Illustrator/Photoshop afterward.

## Hardware / running it
Same as LonnieAI: needs a GPU (local ≥12 GB VRAM for SDXL, or a hosted Comfy Cloud instance — not
runnable in this repo's container). The workflow above is portable; see `comfyui/` for a starter
JSON wired to Drop 4 (the manatee-zone sign, since it's the clearest photo-referenced case).
