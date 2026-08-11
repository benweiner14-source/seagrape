# seagrape

**Seagrape Supply Co.** — bespoke lifestyle apparel capsules for private country clubs. Pilot
client: Admirals Cove Golf & Yacht Club (Jupiter, FL). Full context: `PROJECT_BRIEF.md`.

## Repo layout

```
PROJECT_BRIEF.md            # full project brief — brand, business model, capsule + lookbook plan
capsules/admirals-cove/drops/ # generated capsule graphics (3 back designs + chest burgee)
capsules/admirals-cove/refs/  # Ben's real reference photos (manatee sign, burgee)
references/lifestyle/       # real lookbook-aesthetic reference images (Ralph Lauren/J.Crew/Lafarve)
comfyui/                     # starter ComfyUI workflow JSON + beginner import guide
docs/                        # comfyui-*.md — Comfy Cloud MCP setup, node-graph plan, handoff brief
```

**Capsule structure:** 3 shirts, each with a full illustrated graphic on the **back** plus a
small universal Admirals Cove burgee logo on the **left chest**. (A 5th drop, channel markers,
was cut.) See `PROJECT_BRIEF.md`'s "The Capsule" section for the full construction decision.

## Image generation (ComfyUI / Comfy Cloud)

Capsule graphics are generated via ComfyUI (Comfy Cloud), same setup as the LonnieAI project:

1. **Set up the Comfy Cloud MCP on your local Claude Code** — `docs/comfyui-mcp-setup.md`
   (must be local; the web/cloud session can't do the browser OAuth).
2. **Read the handoff brief** — `docs/comfyui-handoff.md` — self-contained brief covering what's
   generated/approved already, what's pending (mainly a small-scale resize of the chest burgee),
   and the hard constraints (locked color palettes, flat vintage-woodcut style).
3. **Node-graph plan** — `docs/comfyui-workflow.md` — two paths: a fast partner-node test (no
   setup) and a full SDXL + style LoRA + ControlNet fallback for real control.
4. **Starter workflow** — `comfyui/seagrape-manatee-zone-img2img.json` + its import guide, wired
   to the Manatee Zone design as the first thing to test since it has the clearest photo reference.

Note: all output generated so far actually went through **Higgsfield directly**, not Comfy — see
`docs/comfyui-handoff.md` for the current read on whether the full Comfy pipeline is still needed.
Reference photos for Drop 4 and the Drop 3 chest-logo resize still need to be added to
`capsules/admirals-cove/refs/` — see that folder's README.
