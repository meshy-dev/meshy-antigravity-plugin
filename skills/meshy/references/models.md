# Choosing models

Geometry `ai_model` plus texture `texture_model`, by project:

- Detailed hero asset, product render, cinematic prop: `meshy-7.1` + `meshy-7` (PBR, up to 8K)
- Game character or prop with a face budget: `meshy-t2.5` (smart topology, set `target_polycount`) + `meshy-n1`
- Many props or user-generated content: `meshy-t2` + `meshy-n1`
- Many drafts at low cost: `meshy-6-lite` + `meshy-6-lite`

Prices come from `get_balance` at call time and cover default parameters only. For any other model or option, say the price isn't listed and may differ; never quote a number from memory. Reference: https://docs.meshy.ai/en/api/models and https://docs.meshy.ai/en/api/pricing
