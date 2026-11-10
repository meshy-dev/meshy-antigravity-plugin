# Changelog

## [0.1.0] - Unreleased

### Added

- First release of the Meshy plugin for Antigravity. It connects to Meshy's hosted MCP server
  (`https://mcp.meshy.ai/mcp`) with a Meshy API key, which Antigravity's setup dialog asks for when
  the plugin is turned on. The key needs a paid Meshy plan and must not be restricted to an IP
  allowlist. Nothing is installed locally, and Node.js is not needed.
- Tools from the hosted server: text to 3D (preview and refine), image to 3D, texturing a model
  the user already has, text to image, task status and task lists, model download as GLB, FBX,
  OBJ or USDZ, credit balance, and image uploads. The three tools that only work inside ChatGPT
  (`open_meshy_studio`, `show_model`, `app_image_to_3d`) are turned off.
- The `meshy` skill. It asks what the model is for before choosing models, and before any paid
  step it shows the tools, models and credits and waits for a yes. Prices come from `get_balance`;
  when a model or option isn't listed there, it says so. It makes a concept image first when the
  user wants a specific look, sends local images only to Meshy (through `create_upload`), writes
  a fresh `request_id` for each generation, and checks the task list before retrying a timed-out
  task, so nothing is charged twice. It says when an FBX download is a zip with its textures.
  `references/models.md` pairs geometry and texture models by project.
