# seagrape

**Seagrape Supply Co.** — bespoke lifestyle apparel capsules for private country clubs. Pilot
client: Admirals Cove Golf & Yacht Club (Jupiter, FL). Full context: `PROJECT_BRIEF.md`.

## Repo layout

```
PROJECT_BRIEF.md            # full project brief — brand, business model, all 5 capsule drops
capsules/admirals-cove/refs/  # Ben's real reference photos (channel markers, manatee sign, burgee)
comfyui/                     # starter ComfyUI workflow JSON + beginner import guide
docs/                        # comfyui-*.md — Comfy Cloud MCP setup, node-graph plan, handoff brief
```

## Image generation (ComfyUI / Comfy Cloud)

Capsule graphics are generated via ComfyUI (Comfy Cloud), same setup as the LonnieAI project:

1. **Set up the Comfy Cloud MCP on your local Claude Code** — `docs/comfyui-mcp-setup.md`
   (must be local; the web/cloud session can't do the browser OAuth).
2. **Read the handoff brief** — `docs/comfyui-handoff.md` — self-contained brief covering what's
   generated/approved already (Drop 2), what's pending, and the hard constraints (locked color
   palettes per drop, flat vintage-woodcut style, exact anatomy/composition rules where relevant).
3. **Node-graph plan** — `docs/comfyui-workflow.md` — two paths: a fast partner-node test (no
   setup) and a full SDXL + style LoRA + ControlNet fallback for real control.
4. **Starter workflow** — `comfyui/seagrape-manatee-zone-img2img.json` + its import guide, wired
   to Drop 4 (Manatee Zone) as the first thing to test since it has the clearest photo reference.

Reference photos for the photo-based drops (1, 4, 5) still need to be added to
`capsules/admirals-cove/refs/` — see that folder's README.
