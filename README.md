# .github

Organization profile and shared product direction for [tj-agents](https://github.com/tj-agents).

Read [the product vision](VISION.md) when discussing what the application is being designed to become.
It separates the intended public product from recommendations and current implementation. Agent-facing
instructions start at [AGENTS.md](AGENTS.md).

`.agents/repository.json` holds the defaults for every tj-agents repository, one section each. A
repository overrides a section by committing that section in its own `.agents/repository.json`.

- `access` turns on the tomjseery-bot GitHub App for agents, through the
  [tj-agents GitHub access gate](https://github.com/tj-agents/github#github-access-gate). A repository opts out with
  `"access": {"method": "human"}`.
- `merge` is the default merge policy: no approval, agents may merge once the required checks pass, and
  nobody pushes to the default branch outside a pull request. A repository's `merge` section replaces it
  entirely. The schema is
  [github-actions:merge-policy](https://github.com/tj-agents/github-actions/blob/main/.agents/github-actions/utility/merge-policy/SKILL.md),
  and tj-agents/github's `github:configuration` applies it.
