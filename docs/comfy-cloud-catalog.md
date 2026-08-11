# Comfy Cloud catalog — what's available + chosen path

**Status: template, not yet filled in.** This web session has no Comfy Cloud MCP access (same
limitation LonnieAI hit — browser OAuth can't happen from here). The first thing local Claude
Code should do after connecting (`docs/comfyui-mcp-setup.md`) is run `search_models` and fill in
the sections below, following the shape of LonnieAI's `docs/comfy-cloud-catalog.md` as a
reference for what this doc should look like once populated.

## To fill in after `search_models`
- **Checkpoints available** — which SDXL/Flux checkpoints are on the plan, and whether any lean
  illustrative/print/vector rather than photoreal by default.
- **Style options** — any existing woodcut / linocut / vintage-poster / screen-print LoRA in the
  catalog. (LonnieAI's catalog had none of this kind — anime and photoreal only — so budget time
  to check `docs/comfy-cloud-loras.md`'s candidates for upload if the gap repeats here.)
- **ControlNet availability** — Canny and/or Lineart preprocessors, needed for the photo-referenced
  drops (1, 4, 5) per `docs/comfyui-workflow.md`.
- **Custom LoRA upload** — confirm whether the plan supports it via MCP (`upload_file` was
  images-only on LonnieAI's plan; may need the web dashboard instead) and note the billing tier.

## Known constraint carried over from LonnieAI
No `get_billing_status`-equivalent guarantee — check the Comfy Cloud web dashboard directly for
credits/tier if `get_billing_status` isn't available as a tool.

## Chosen path (fill in once tested)
Record here which of Path A (partner node, no setup) or Path B (SDXL + style LoRA + ControlNet)
from `docs/comfyui-workflow.md` actually produced the locked-style, on-palette result, and what
settings it took — this becomes the repeatable recipe for the remaining drops and future clubs.
