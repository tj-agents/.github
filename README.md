# .github

Organization profile and shared product direction for [tj-agents](https://github.com/tj-agents).

Read [the product vision](VISION.md) when discussing what the application is being designed to become.
It separates the intended public product from recommendations and current implementation. Agent-facing
instructions start at [AGENTS.md](AGENTS.md).

`.github/merge-policy.json` is the default merge policy for every tj-agents repository without its own:
no approval, agents may merge once the required checks pass, and nobody pushes to the default branch
outside a pull request. A repository overrides it entirely by committing its own
`.github/merge-policy.json`. The schema is
[github-actions:merge-policy](https://github.com/tj-agents/github-actions/blob/main/.agents/github-actions/utility/merge-policy/SKILL.md),
and tj-agents/github's `github:configuration` applies it.
