# tj-agents product vision

**Direction recorded 17 November 2026.** This document owns the shared product direction. It distinguishes
Tommy's stated destination from recommendations and implemented behavior. It is not an implementation plan.

## The destination

Build a coherent product that other people can download, install and use to run coding agents in their own
projects. The organization and its repositories should serve that product, with a clear entry point and
an understandable installation and first-use experience.

Tommy's personal setup is an initial use case. The product must work for someone who has none of his
accounts, credentials, directories, organizations or conventions. Users bring their own agent accounts,
repositories and permissions; projects select the policies and standards that apply to them.

[T3 Code](https://github.com/pingdotgg/t3code) is an inspiration for the product category: one application
that controls coding agents people already use. That comparison does not select its architecture, interface,
license, business model or feature list for tj-agents.

## The product boundary

The managed runtime should own the lifecycle of work across Claude Code and Codex: starting a session,
establishing its project and ownership, coordinating handoffs, preserving recovery state, delivering results
and safely closing completed work. Existing host capabilities remain the foundation.

Language models make judgments about the task. Deterministic runtime operations enforce process identity,
ownership, worktree location, state transitions and cleanup. A successful experience must not depend on
remembering a sequence of incidental terminal commands or discovering a missing skill after delivery.

All managed launch paths should reach the same lifecycle implementation. Launching a child by handoff must
preserve the same completion and recovery guarantees as starting a session directly. A later graphical
interface, if selected, should use that same implementation.

## Managed entry points: recommendation awaiting a decision

Use `tj` as the product's explicit front door. The proposed everyday command shape is:

```text
tj run claude
tj run codex
```

That is a proposed interface, not a claim about the installed parser. The currently documented wrapper
syntax includes the argument separator:

```text
tj run -- claude
tj run -- codex
```

The recommendation is to make managed launches explicit and easy to use, while retaining the providers'
executables as dependencies with their own authentication and native features. Invoking a provider directly
does not establish a managed tj session. Product lifecycle guarantees require the managed entry point.

The final command names and argument handling need an explicit interface decision and implementation in
[CLI](https://github.com/tj-agents/cli). This document changes no executable, shell binding or launcher.

## What a reliable product must achieve

| Concern | Intended user experience |
| --- | --- |
| Installation | A new user can install from published instructions without Tommy's machine or private state. |
| Host choice | Claude Code and Codex share lifecycle guarantees while preserving their native capabilities. |
| Project policy | Users and projects select relevant standards and permissions; Tommy's personal profile is optional. |
| Ownership | Sessions and handoffs have recorded owners, with a clear distinction between active, waiting and completed work. |
| Worktrees | Managed creation uses one enforced location and creation path, with safe ownership and cleanup. |
| Completion | Reporting a finished result, completing its work item and requesting session closeout form a verified completion path. |
| Recovery | Interruptions preserve unfinished work and its ownership so it can be resumed without competing writers. |
| Evidence | Completion is supported by recorded results and observable runtime behavior, including real handoff launches. |

Closing a finished session must preserve explicit keep-open instructions, genuine pending work and authored
changes. Generated instruction state must not make an otherwise completed checkout fail cleanup. These are
product acceptance requirements; their presence here does not establish that every installed path meets them.

## Scope of the current direction

| Subject | State |
| --- | --- |
| A product other people can download and use | Tommy's stated destination, 17 November 2026 |
| A proper public organization supporting that product | Tommy's stated destination, 17 November 2026 |
| T3 Code as an inspiration | Tommy's stated comparison, 17 November 2026 |
| `tj run claude` and `tj run codex` as the preferred interface | Recommendation in response to Tommy's question; decision pending |
| Existing `tj run` wrapper and lifecycle mechanics | Implemented components; see their source owners for exact behavior and limitations |
| A desktop, web, mobile or remote interface | Not selected by this vision |
| New branding, licensing, pricing or hosted services | Not selected by this vision |

## How to use this document

Read this before discussing product vision, the public user experience or architecture that changes the
product boundary. Assess proposals against a new user's experience, portability and lifecycle reliability.
Keep implementation details with their source owner and link back here rather than maintaining another
version of the vision. Record a new direction only when Tommy decides it; keep suggestions labelled.

For the current system, use [shared reference documentation](https://github.com/tj-agents/docs).
[Agent](https://github.com/tj-agents/agent) owns host/session integration and coordination;
[CLI](https://github.com/tj-agents/cli) owns deterministic process, terminal and worktree mechanics;
[Core](https://github.com/tj-agents/core) owns shared workflow and engineering guidance. The repositories'
own contracts remain authoritative for their implementation.

Sources: Tommy's product-direction request on 17 November 2026; the
[CLI usage documentation](https://github.com/tj-agents/cli#tj-run-the-agent-tabs-root-process) and
[T3 Code's product description](https://github.com/pingdotgg/t3code), checked 17 November 2026.
