# Research: similar projects, tools, and guides

Compiled Oct 2026. Items marked *(unverified)* come from vendor marketing or community posts. They have not been checked against official docs.

## Closest prior art

| Project | What it is | What to borrow |
|---|---|---|
| **OpenGame** ([paper 2604.18394](https://hyper.ai/en/papers/2604.18394), [repo](https://github.com/RyensX/OpenGame)) | Open-source agentic framework that generates playable 2D Phaser web games end to end from a prompt. Ships GameCoder-27B and OpenGame-Bench (150 tasks; scores build health, visual usability, and intent alignment) | **The core blueprint.** Six phases: classify → scaffold → GDD → assets → implement → headless verify. *Template Skill* (evolving skeletons with hooks) and *Debug Skill* (a living error → fix protocol). Weakest on strategy and puzzle games. Does **not** publish or market |
| **Roblox Build** ([Insider Gaming](https://insider-gaming.com/robloxs-new-ai-tool-builds-games-from-text-prompts/), [OpenCritic](https://opencritic.com/news/34651/roblox-players-will-soon-be-able-to-build-games-using-ai-text-prompts)) | Roblox's own prompt-to-game prototype tool in the mobile app. Public alpha opened in New Zealand on Jul 28, 2026. Games made with Build are visible only to age-verified users aged 16+ | Validates the concept. Note the extra audience restriction on Build-made games: generate through Studio and Open Cloud instead |
| **Roblox Assistant + Studio MCP** ([MCP docs](https://create.roblox.com/docs/studio/mcp), [DevForum update](https://devforum.roblox.com/t/studio-mcp-server-updates-and-external-llm-support-for-assistant/4415631)) | Studio's built-in MCP server exposes tools for scripts, assets, Luau execution, playtesting, input simulation, and screen capture. Assistant can plan, build, and test, and it supports external LLMs | **The Studio-plane foundation.** Claude Code is a "Quick connect" client |
| **Ropilot** ([site](https://ropilot.ai/roblox-ai-builder), [how-to](https://ropilot.ai/blog/how-to-make-a-roblox-game-with-ai)) | A commercial Studio agent that reads the game, writes Luau, applies changes, and playtests | Argues that incremental agentic building beats one-shot full-game generation *(vendor claim)* |
| Lemonade, SuperbulletAI, BloxBot, PromptBlox, Rebirth ([comparison](https://ropilot.ai/blog/lemonade-vs-superbullet-vs-ropilot)) | Other commercial Roblox AI game builders | Competitive landscape. The comparison page is written by a competitor *(unverified)* |

## Roblox Studio MCP servers (community)

- [Roblox/studio-rust-mcp-server](https://github.com/Roblox/studio-rust-mcp-server): official, **archived Apr 3, 2026** in favor of the built-in server.
- [boshyxd/robloxstudio-mcp](https://mcpservers.org/th/servers/boshyxd/robloxstudio-mcp): explore, read, and edit scripts. Has a read-only inspector mode.
- [hope1026/weppy-roblox-mcp](https://mcpservers.org/servers/hope1026/weppy-roblox-mcp): about 21 tools and 140+ actions, multi-place support, automated playtest. AGPL-3.0, with a paid Pro tier.
- [Meganugger/roblox-studio-mcp](https://glama.ai/mcp/servers/Meganugger/roblox-studio-mcp): batch building, dry-run script edits.
- [el4cteo/rbx-studio-mcp](https://mcpservers.org/servers/el4cteo/rbx-studio-mcp): an npx-installable server plus its own Studio plugin.
- [roblox-devproducts-mcp](https://glama.ai/mcp/servers/oh7wjtj05e): creates game passes and developer products through Open Cloud.

## Roblox Open Cloud: APIs used by the pipeline

- **Place publishing:** [usage guide](https://create.roblox.com/docs/cloud/open-cloud/usage-place-publishing). Needs the universe ID, the place ID, and a key with `universe-places` write access.
- **Luau Execution (headless tests):** [reference](https://create.roblox.com/docs/cloud/reference/features/luau-execution.md), [beta announcement](https://devforum.roblox.com/t/beta-open-cloud-engine-api-for-executing-luau/3172185).
  - Tasks run up to 5 minutes, with 10 concurrent tasks per place.
  - Small per-key rate limits.
  - The environment differs from Studio ([thread](https://devforum.roblox.com/t/luau-open-cloud-execution-should-provide-an-environment-similar-to-studio/3955280)).
- **Universes API (name, description, restart servers):** [announcement](https://devforum.roblox.com/t/open-cloud-universes-api/2865540). Thumbnails use the legacy [Game Internationalization v1](https://create.roblox.com/docs/cloud/legacy/gameinternationalization/v1) API.
- **Game passes and developer products:** [game passes](https://create.roblox.com/docs/fr-fr/cloud/features/game-passes), [community thread](https://devforum.roblox.com/t/external-api-to-roblox-developer-products/4618120).
- **Advertising (Ads API):** [guide](https://create.roblox.com/docs/cloud/guides/advertising).
  - Base path `ads-management/v1`.
  - Supports the ENGAGEMENT objective only, with DAILY or LIFETIME budgets in micro-USD.
  - Campaigns go through policy review before serving.
  - Requests accept an idempotency key.
- **Analytics Query API (beta):** [community writeup](https://devforum.roblox.com/t/open-cloud-analytics-query-api-is-live-beta-%E2%80%94-tested-documented-with-a-client/4753664), [analytics docs](https://create.roblox.com/docs/production/analytics/developer-statistics).
- **Docs index for LLM grounding:** [create.roblox.com/docs/cloud/llms.txt](https://create.roblox.com/docs/cloud/llms.txt).
- **Wrappers:**
  - [rblx-open-cloud (Python)](https://pypi.org/project/rblx-open-cloud/0.4.3)
  - [rbxcloud (Rust CLI)](https://cdn.jsdelivr.net/npm/rbxcloud@1.2.0/README.md)
  - [opencloud.js](https://github.com/ItsRune/opencloud.js)
  - [RoZod](https://www.mintlify.com/AlroviOfficial/RoZod/api/opencloud/overview)

## CI/CD guides for Roblox

- [Roblox/place-ci-cd-demo](https://worker-github.zxx930427.workers.dev/Roblox/place-ci-cd-demo): Selene, StyLua, Luau Execution tests, and a Rojo deploy. Archived Sep 2024, but still a good reference.
- [Nevermore deploy CLI](https://quenty.github.io/NevermoreEngine/docs/deploy): Rojo build → Open Cloud upload → optional publish.
- [Mantle continuous deployment](https://mantledeploy.vercel.app/docs/continuous-deployment): infrastructure-as-code for experiences.
- [DevForum: Rojo + Wally + TestEZ CI](https://devforum.roblox.com/t/cicd-setup-with-rojo-wally-testez/3610450): install Wally packages before `rojo build`.
- [DevForum: automating publishing with partially managed Rojo](https://devforum.roblox.com/t/how-to-automate-place-publishing-with-partially-managed-rojo/2443196).

## Generative 3D

- [Roblox Cube (3D/4D)](https://corp.roblox.com/newsroom/2025/03/introducing-roblox-cube): an open-sourced foundation model, available as a mesh-generation API in Studio and in-experience.
- [4D generation beta](https://devforum.roblox.com/t/beta-4d-generation-unlock-new-types-of-gameplay/4331818): interactive, scripted multi-mesh objects, generated in about 20–40 seconds.

## Policy

- [Roblox Terms of Use updates](https://devforum.roblox.com/t/updates-to-the-roblox-terms-of-use-may-2024/2971640). The AI terms were folded into the main Terms in April 2026 ([change log](https://conductatlas.com/change/2026-04-09-roblox-roblox-terms-of-use-267/)).
- Read the Community Standards and the advertising policy before enabling automated public release or ads.
