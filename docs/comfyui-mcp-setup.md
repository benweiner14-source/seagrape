# Connect Claude Code → Comfy Cloud (official MCP)

Comfy Cloud ships an **official Claude Code plugin / MCP server**, so a *local* Claude Code can
drive it directly (build workflows, run them, pull outputs). Source:
https://docs.comfy.org/development/cloud/mcp-server

This is the same setup used on the LonnieAI project (`benweiner14-source/lonnieai`) — same steps,
pointed at this repo instead.

> **Must be LOCAL Claude Code**, not this cloud/web session. The web session can't do the browser
> sign-in or reach the endpoint. Run the Claude Code CLI on your own computer.

## Prerequisites
- A **Comfy Cloud account** — https://cloud.comfy.org
- **Claude Code CLI installed locally** (`npm i -g @anthropic-ai/claude-code`, then `claude`)

## Step 1 — Get this repo locally
So local Claude Code has the drop prompts, reference photos, starter workflow, and docs:
```bash
git clone https://github.com/benweiner14-source/seagrape.git
cd seagrape
git checkout claude/seagrape-repo-setup-gfmnyb
claude                      # start Claude Code in the repo
```

## Step 2 — Add the Comfy Cloud MCP
**Option A — plugin (recommended):** inside Claude Code, run:
```
/plugin marketplace add Comfy-Org/comfy-skills
/plugin install comfy-cloud@comfy-skills
```
**Option B — direct MCP (no plugin):**
```bash
claude mcp add --transport http comfy-cloud https://cloud.comfy.org/mcp
```

## Step 3 — Authenticate
Run `/mcp` → select **comfy-cloud** → **Authenticate**. Your browser opens for sign-in; tokens
refresh automatically after that.

## Step 4 — Verify
Ask Claude Code to call `get_server_info` (and `get_billing_status`). If they return, you're wired.

## What the MCP can do (tools)
- **Discovery:** `search_templates`, `get_template`, `search_models`, `search_nodes`, `get_node`, `cql`
- **Generation:** `run_template`, `submit_workflow`, `partner_generate`, `upload_file`
- **Jobs:** `get_job_status`, `wait_for_job`, `get_output`, `cancel_job`
- **Workflows:** `list_saved_workflows`, `save_workflow`, `run_saved_workflow`
- Plugin slash-commands: `/comfy-cloud:generate-image`, `…:upscale-image`, `…:search-models`, etc.

## Step 5 — First run (what to tell local Claude Code)
Point it at the plan already written for this:
> Read `PROJECT_BRIEF.md`, `docs/comfyui-handoff.md`, and `docs/comfy-cloud-catalog.md` first —
> they record the five capsule drops (prompts already written), what's already been generated
> (Drop 2, via Higgsfield, approved — treat as the style bar to match), and the currently
> recommended path. Respect the hard constraints: locked per-drop color palettes, flat
> screen-print-safe illustration (no gradients/photoreal shading), legible club name/date text,
> no invented placeholder text baked into the art.

## Notes on the LoRA-tier concern
Use `search_models` to see which checkpoints/LoRAs Comfy Cloud exposes on your plan, and
`get_billing_status` for credits/tier. If a good vintage-woodcut/illustration LoRA isn't in the
catalog, see `docs/comfy-cloud-loras.md` for candidates to upload, or fall back to a strong
prompt on a stylized checkpoint.

## If you'd rather I (this web session) drive it
I can't — this cloud session can't do the browser OAuth or reach cloud.comfy.org. Driving Comfy
Cloud has to happen from your local Claude Code (or another Claude with the MCP authenticated),
same as the LonnieAI project.
