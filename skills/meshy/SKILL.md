---
name: meshy
description: Generates 3D models and reference images with Meshy (text to 3D, image to 3D, texturing) with explicit credit-cost confirmation, then downloads GLB, FBX, OBJ or USDZ files. Use when the user asks to create, texture or export a 3D model with Meshy.
---

# Meshy for Antigravity

Use only this plugin's `meshy` MCP connection. Every generation spends the user's Meshy credits, so plan first, show the cost, and wait for an explicit yes before any paid call.

## Steps

1. **Ask what the model is for** (game asset, hero render, print, AR) if the user has not said. A game asset or a face budget means smart topology (`ai_model` `meshy-t2.5` or `meshy-t2` with `target_polycount`).
2. **Plan and confirm.** Call `get_balance` for the live price list and the balance. Its prices cover default parameters only: quote those, and for any other model or option (such as `meshy-t2`, `meshy-t2.5`, `meshy-6-lite` or an 8K texture) say the price isn't listed instead of guessing. Name each paid tool, its model and its credits, and wait for the user's explicit agreement. A change of model, parameters or quantity needs a new confirmation.
3. **Worded prompts go image-first** when the user wants a specific look: `text_to_image`, show the result, and only after they accept it call `image_to_3d` with that image. Call `text_to_3d_preview` directly when the user asks to skip the image.
4. **Generate.** `text_to_3d_preview` then `text_to_3d_refine`, or `image_to_3d`, or `texture_model` for a model the user already has. For `request_id`, write a new random version-4 UUID yourself for every new generation, without running a command for it; reuse it only when retrying the same generation. Make each one unpredictable, never a pattern such as `a1b2c3d4-e5f6-…` or one used before: for 30 days the server answers a repeated `request_id` with the earlier result instead of a new model.
5. **Wait and deliver.** Poll `get_task` until it succeeds, then `download_model` in the format the user asked for and save it where they said. An FBX download is a zip that holds the model and its texture images; say so, and name the files inside. Report the task id and the credits the task consumed.

## Rules

- Never ask the user to paste an API key into the chat. The key lives in the plugin's setup dialog only.
- A local image is a workspace file. Send it only to Meshy: call `create_upload` (purpose `image`, its format and exact size in bytes), PUT the file once to `upload_url` with exactly `upload_headers`, then pass `upload_id` as `image_upload_id` (or `texture_image_upload_id`). Never put a user's image on any other host to get a URL, and don't use `image_file`, which only works in ChatGPT.
- Never re-create a task after a timeout or network error without checking `list_tasks` first; the task may exist and be charged already.
- Keep Antigravity's default Ask permission for Meshy tools.
- Download links expire; fetch a fresh one with `download_model` when a link fails.

See [references/models.md](references/models.md) for choosing models.
