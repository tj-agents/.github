# tj-agents

Tommy's way of working, expressed as policy, plus one small tool that runs the work-item lifecycle across
many Claude Code and Codex agents. Everything mechanical that the hosts, git and the trackers already do,
they do: it's a thin deterministic layer — CLI scripts plus thin trigger skills — where judgement skills
hold the conventions and the hosts' native features do the mechanics, with harness parity (every capability
works the same from both hosts).

## How it fits together

- **Profiles decide context.** Every repository in this org is a personal project: GitHub Issues and
  Projects, the bot identity, and Renovate via org-level config. A repository outside this org gets a
  profile injected instead — `work` is generic, employer-agnostic support; `infonetica` holds only what's
  specific to Tommy's current employer (Azure DevOps config, Infonetica conventions). A future employer is
  a new profile, not a lifecycle change. Personal-only automation never reaches work repositories.
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
| [`infonetica`](https://github.com/tj-agents/infonetica) *(private)* | What's specific to Tommy's current employer — Azure DevOps config, Infonetica conventions |
| [`template`](https://github.com/tj-agents/template) | The plugin layout and one generator every repository here is scaffolded from |
| [`marketplace`](https://github.com/tj-agents/marketplace) | The canonical plugin roster and dependency graph both hosts install from |
| [`renovate-config`](https://github.com/tj-agents/renovate-config) | The org-level shared Renovate configuration that keeps cross-repository pins current |
| [`docs`](https://github.com/tj-agents/docs) | Global architecture, cross-repository designs, decisions and roadmaps |
| `python`, `rust`, `cpp`, `dotnet`, `react`, `azure`, `nvim`, `learning`, `github-actions` | Per-stack engineering standards and learning companions, selected as plugins where that stack applies |

## Using it

A repository adopts plugins from [`tj-agents/marketplace`](https://github.com/tj-agents/marketplace) in
its own `.agents/plugins.json`; the profile it selects (`personal`, `work`, or an employer profile like
`infonetica`) decides which tracker its work-item cards live in. See each repository's own README for its
specific commands and skills.
