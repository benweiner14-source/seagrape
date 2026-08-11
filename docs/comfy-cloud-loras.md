# Candidate LoRAs to upload to Comfy Cloud (SDXL 1.0)

**❌ NOT IN USE — kept for historical record only.** Ben decided against LoRAs/ControlNet
entirely (see the note at the top of `docs/comfyui-workflow.md`) — everything runs as GPT Image 2
prompts via Comfy's `partner_generate` node instead. Don't act on anything below this line.

If `docs/comfy-cloud-catalog.md` confirms the same gap LonnieAI hit — no illustrative/print style
in the default catalog, photoreal base only — these are starting candidates to search Civitai for
(free account), matched to the SDXL 1.0 base. **Confirm SDXL 1.0 compatibility before pulling** —
don't use Illustrious, Pony, or SD1.x LoRAs against an SDXL 1.0 checkpoint, they won't load.

## For the vintage woodcut / botanical field guide look (priority — every drop)
Search Civitai for terms close to the brand's actual reference language in `PROJECT_BRIEF.md`:
- **"woodcut" / "linocut" / "block print"** — hand-cut ink-line texture, the core of the look.
- **"vintage travel poster" / "WPA poster style"** — flat color, confident line, period-accurate
  (1930s–60s) graphic feel; good match for the Drop 1 back-graphic composition.
- **"botanical illustration" / "field guide"** — closest match for the logo's tree icon
  specifically; look for SDXL LoRAs trained on antique naturalist plates.
- **"screen print" / "riso" / "risograph"** — flat, limited-color, slightly misregistered texture;
  useful for selling the "actually printable" quality if the base style reads too smooth.

## Usage notes
- **Get the trigger word** from each Civitai model page and put it in the positive prompt — LoRAs
  often need their trigger to activate.
- **Stack sparingly:** one style LoRA is probably enough here (no identity LoRA competing for
  weight, unlike LonnieAI). If stacking two style LoRAs (e.g. woodcut + vintage-poster), keep each
  ≤0.5 so they don't fight.
- **Skip (won't work with an SDXL 1.0 checkpoint):** any "Illustrious", "Pony", or "SD 1.x" LoRA.
- **Downloads may need a Civitai login / API token** — that's on Ben's side.

## Not yet verified
Nobody has run these against Comfy Cloud for this project yet — this list is a starting search
list based on the brand direction in `PROJECT_BRIEF.md`, not a confirmed-working set like
LonnieAI's. Update this file with the actual model names/URLs and weights that test well, same as
LonnieAI's version does.
