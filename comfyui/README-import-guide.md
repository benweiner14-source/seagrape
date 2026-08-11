# ComfyUI — beginner import & run guide (Drop 4, Manatee Zone)

Goal: turn Ben's real photo of the Manatee Zone sign into a print-ready, flat-color vintage
woodcut illustration using ComfyUI — same beginner-friendly approach as LonnieAI's
`zion-cgi-img2img.json`, adapted here since this project has no identity/anatomy constraints to
worry about, just style + composition.

This first workflow (`seagrape-manatee-zone-img2img.json`) is intentionally simple — **only
built-in nodes, nothing to install** — so it just works. Once it runs, we level it up (add a real
style LoRA and/or ControlNet for tighter composition control — see `docs/comfyui-workflow.md`).

---

## What you need first
1. **ComfyUI running** (your Comfy Cloud account, or the desktop app).
2. **One SDXL checkpoint model.** In ComfyUI Manager → "Model Manager", or from Civitai, download
   an SDXL checkpoint. If you only have base `sd_xl_base_1.0.safetensors`, that's fine to start —
   the prompt is doing most of the style work in this simple version.
   - Local install path: `ComfyUI/models/checkpoints/`. On Comfy Cloud, use its model uploader.
3. **Ben's Manatee Zone reference photo**, saved into `capsules/admirals-cove/refs/` (see that
   folder's README — it's not committed to the repo yet, this needs adding first).

---

## Step 1 — Import the workflow
1. Open ComfyUI.
2. Drag **`seagrape-manatee-zone-img2img.json`** from this folder onto the ComfyUI canvas (or
   top-left menu → **Workflow → Open**, and pick the file).
3. You'll see 4 labeled colored groups: **Load model → Reference photo → Prompts → Render+Save**.

> If any node shows up red, it means a value doesn't match your files — that's expected; fix it
> in Step 2. Red because of a *missing node type* shouldn't happen here (all nodes are built-in).

## Step 2 — Point it at your files
1. **Load model group** (top-left, "Load Checkpoint"): click the model dropdown and pick **your**
   SDXL checkpoint. (The file name in the workflow is just a placeholder.)
2. **Reference photo group** ("Load Image"): click **choose file to upload** and upload Ben's
   Manatee Zone sign photo from `capsules/admirals-cove/refs/`.

## Step 3 — Run it
1. Click **Queue Prompt** (or press **Ctrl+Enter**).
2. First run downloads/loads the model (can take a minute). The result appears in the
   **Save Image** node and saves to your `output/` folder.

That's a working woodcut-ish render with **zero custom nodes**. Now tune it.

---

## The one dial that matters most: **denoise**
In the **KSampler** node (Render group) there's a **`denoise`** value (default **0.7**). This is
the photo↔illustration slider:
- **Higher (0.75–0.85):** restyles harder → cleaner break into flat illustration, but drifts
  further from the photo's exact layout.
- **Lower (0.5–0.6):** stays closer to the real photo's colors/composition → risks reading more
  photoreal than illustrated.
Start at 0.7 and nudge until it reads as a flat vintage illustration while still clearly being
*that* sign, on *those* pilings.

Other KSampler knobs: `steps` 30 is fine; `cfg` 7 is fine; `seed` set to "randomize" gives a new
variation each run.

---

## Level-up 1 — add a woodcut/vintage-illustration LoRA (bigger style push)
The workflow already has a **Load LoRA** node, currently **bypassed** (greyed out) so it doesn't
error.
1. Download an SDXL **style LoRA** for the look (see `docs/comfy-cloud-loras.md` for search
   terms: "woodcut", "linocut", "vintage travel poster"). Put it in `ComfyUI/models/loras/`.
2. Click the **Load LoRA** node → set its LoRA dropdown to that file.
3. **Un-bypass it:** click the node and press **Ctrl+B** (bypass toggles off; node turns normal).
4. Re-queue. Adjust its `strength` (0.6–0.9) for more/less style.

## Level-up 2 — hold the composition harder (ControlNet)
When the plain img2img drifts the sign's geometry too far, add a **ControlNet (Canny)** node fed
by the same reference photo. That locks the pilings/sign shape while the LoRA + prompt still
carry the full restyle — the best of both worlds. See `docs/comfyui-workflow.md`'s Path B for the
full node plan.

---

## Reusing this for the other drops
Duplicate this file, swap the **Load Image** for that drop's reference photo (Drop 1, Drop 5 —
skip this node entirely for Drop 3 / the logo, which have no photo reference), and swap the
positive/negative prompt text for that drop's from `PROJECT_BRIEF.md`. Keep the color-count line
in the prompt exact — that's the one thing that has to hold for a screen print to work.

## If something breaks
- **Red node / "missing"**: tell me the node name; for this file it should only be a mismatched
  model/LoRA/image filename → reselect it in the dropdown.
- **Output looks like the plain photo**: raise `denoise`, and/or enable the LoRA (Level-up 1).
- **Colors don't match the locked palette**: lower `cfg` slightly, restate the exact color list at
  the end of the prompt, not just the start.
- Send a screenshot of the result + your denoise value and it can be diagnosed from there.
