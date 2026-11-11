# Meshy for Antigravity

Generate 3D models with [Meshy](https://www.meshy.ai) from Antigravity: text or image to 3D, texturing, reference image generation, and download as GLB, FBX, OBJ or USDZ.

The plugin connects to Meshy's hosted MCP server (`https://mcp.meshy.ai/mcp`) and bundles the `meshy` skill, which plans each job, shows the credit cost and waits for your confirmation before any paid step.

## Requirements

- A paid Meshy plan with credits. Generation spends your Meshy credits.
- A Meshy API key from the [Developer Console](https://www.meshy.ai/developers/keys), without an IP allowlist. The hosted server refuses keys restricted to an IP allowlist.
- Antigravity App or Antigravity CLI. No Node.js or local install is needed.

## Setup

1. Install the plugin. It stays disabled until configured.
2. Turn it on under **Customizations → Installed → Meshy** (in the CLI: `/plugin`, then space). Antigravity opens a setup dialog asking for your Meshy API key, with a link to create one.
3. Ask: "What's my Meshy credit balance?"

Never paste an API key into the chat.

## Try it

- Turn this reference image into a textured 3D model and download it as GLB.
- Generate a low-poly treasure chest for my game and export it as FBX.
- Make a concept image of a sci-fi helmet, then turn it into a 3D model.

## Costs and approvals

Before any paid step the skill shows the tools, models and credits involved and waits for an explicit yes. Reads (`get_balance`, `get_task`, `list_tasks`) and uploads are free. `download_model` spends no credits, but each download counts toward your plan's monthly download limit where it has one.

The skill quotes the prices `get_balance` returns: each generation at its default settings, plus texturing by model and resolution. For anything not listed there it says the price isn't listed. Full price list: https://docs.meshy.ai/en/api/pricing

To send a local image or save a model, the agent runs `curl`. Antigravity asks you to approve each command unless you allow it.

## Troubleshooting

- **401 / key rejected**: the key is mistyped or revoked. Create a new key and update it under Customizations → Installed → Meshy.
- **403 ip_not_authorized**: the key is restricted to an IP allowlist, which the hosted server does not accept. Create a key without one.
- **402 plan_upgrade_required**: generation needs a paid Meshy plan.
- **429**: the hosted server allows 20 requests per second per key. Wait and retry.
- **Task still running**: ask the agent to keep polling the same task instead of starting a new one.
- **RESOURCE_EXHAUSTED (code 429) from the model**: that is Antigravity's own model quota, not Meshy. Your Meshy task keeps running. When the quota resets, ask the agent to check the task and download it.
- **FBX arrives as a .zip**: the zip holds the FBX file and its texture images. Keep them together.

## Data and privacy

Prompts, images and models you send are processed by Meshy under the [Privacy Policy](https://www.meshy.ai/privacy-policy) and [Terms](https://www.meshy.ai/terms-of-use). A local image goes only to Meshy: the agent uploads it to Meshy's own storage with `create_upload`, never to another host. The key is stored by Antigravity, never in this repository.

## Support

- Docs: https://docs.meshy.ai/en/api/ai
- Discord: https://discord.gg/meshy
