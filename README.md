# .github
Organization profile for tj-agents.

`.github/merge-policy.json` is the default merge policy for every tj-agents repository without its own:
no approval, agents may merge once the required checks pass, and nobody pushes to the default branch
outside a pull request. A repository overrides it entirely by committing its own
`.github/merge-policy.json`. The schema is
[github-actions:merge-policy](https://github.com/tj-agents/github-actions/blob/main/.agents/github-actions/utility/merge-policy/SKILL.md),
and tj-agents/github's `github:configuration` applies it.
