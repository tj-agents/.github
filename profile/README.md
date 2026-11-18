# tj-agents

Building an installable product for running and coordinating coding agents, starting with Claude Code
and Codex. The intended experience works with users' own accounts, repositories and selected policies.

Read the [shared product vision](https://github.com/tj-agents/.github/blob/main/VISION.md) for the destination,
the proposed managed entry points and the distinction between that direction and what is implemented today.
The existing repositories provide the runtime, host integrations and selectable standards behind that work.

## How it fits together

- **Profiles decide context.** Projects explicitly select the policies and tracker that apply to them.
  Personal-project preferences and employer-specific configuration stay in their selected profiles;
  the shared runtime serves those contexts without assuming Tommy's accounts or conventions.
- **Load what you use.** Standards are split into plugin families a repository selects — language/stack
  families (`.NET`'s `efcore`, Rust's `seaorm`/`rust-sqlx`, …) apply only where that stack is detected.
- **Lifecycle verbs, not judgement.** `tj start`, `tj status`, `tj reload` and `tj item` are deterministic
  CLI commands; `tj run` owns each terminal tab and its automatic closeout. The model decides *what* to
  build and *whether it's done*, then calls the verb.
- **Separate repositories, joined by pinned dependencies.** Each repository owns one responsibility and
  publishes an importable package; every cross-repository use is a pinned dependency that Renovate bumps —
  never a path-loaded sibling checkout.

Some of this — native plugin distribution with a fail-closed staleness check, and org-level Renovate — is
still landing; repositories note it individually where it isn't finished yet.

## Repository map

| Repository | Owns |
|---|---|
| [`agent`](https://github.com/tj-agents/agent) | Agent-session lifecycle: `tj start`/`status`/`reload`, host adapters for Claude and Codex, machine install |
| [`agent-store`](https://github.com/tj-agents/agent-store) | The link store between tracker work items and agent sessions — SQLite/SeaORM, a Rust library and a JSON CLI |
| [`cli`](https://github.com/tj-agents/cli) | Deterministic OS/terminal mechanics: the tab-owning `tj run` wrapper and closeout, `tj_hook`, `cr`, `f` |
| [`core`](https://github.com/tj-agents/core) | Judgement skills over that lifecycle layer: `base`, `workflow`, `engineering`, `docs` |
| [`work-items`](https://github.com/tj-agents/work-items) | The tracker interface and canonical states — GitHub and Azure DevOps adapters, the `tj item` CLI |
| [`github`](https://github.com/tj-agents/github) | General-purpose GitHub access, collaboration and configuration utilities |
| [`personal`](https://github.com/tj-agents/personal) | The personal-project profile: GitHub tracker selection, the bot GitHub App identity, `tj approve` |
| [`work`](https://github.com/tj-agents/work) | The employer-agnostic work profile and communication workflows |
| [`company`](https://github.com/tj-agents/company) *(private)* | A generic employer profile: a templated tech stack, tracker and delivery conventions to fill in per employer |
| [`template`](https://github.com/tj-agents/template) | The plugin layout and one generator every repository here is scaffolded from |
| [`marketplace`](https://github.com/tj-agents/marketplace) | The canonical plugin roster and dependency graph both hosts install from |
| [`renovate-config`](https://github.com/tj-agents/renovate-config) | The org-level shared Renovate configuration that keeps cross-repository pins current |
| [`docs`](https://github.com/tj-agents/docs) | Reference documentation for current architecture and cross-repository responsibilities |
| `python`, `rust`, `cpp`, `dotnet`, `react`, `azure`, `nvim`, `learning`, `github-actions` | Per-stack engineering standards and learning companions, selected as plugins where that stack applies |

## Using it

A repository adopts plugins from [`tj-agents/marketplace`](https://github.com/tj-agents/marketplace) in
its own `.agents/plugins.json`; the profile it selects (`personal`, `work`, or an employer profile like
`company`) decides which tracker its work-item cards live in. See each repository's own README for its
specific commands and skills.
