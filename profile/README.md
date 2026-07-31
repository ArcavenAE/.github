# Arcaven Agentic Engineering

[![Arcaven Agentic Engineering ecosystem map showing content packs, fleet orchestration, agent sessions, memory, evaluation, triage, onboarding, and work tracking](assets/arcavenae-ecosystem.png)](assets/arcavenae-ecosystem.png)

*The ArcavenAE ecosystem. Select the map to view it at full resolution.*

A toolkit for running many AI agents as an organization: schedule and
supervise them, keep what they learn, retrieve it when it matters, reach
them on any host, configure them from signed packages, and measure what
they produce. Small tools with boring seams (YAML, CLI flags, NDJSON,
tmux, JSONL, signed tarballs). Each is independently useful; none
requires another.

Not a framework, not a SaaS. Local-first and user-sovereign: your tools,
your data, your credentials, your workflow.

## Why

Organizations exist to make limited workers collectively effective. LLM
agents are the first workers whose limits are explicit and metered:
context in tokens, spend in dollars, attention in queue depth. That
turns organizational design from management folklore into an engineering
discipline with measurable inputs; you can A/B test a team structure.
Most problems the agent field is discovering (specialization,
coordination, succession, attention scarcity, provenance of authority)
have long-tested solutions. We look those up and test them, rather than
rediscover them one outage at a time.

## The tour

| Project | Function | State |
|---|---|---|
| [marvel](https://github.com/ArcavenAE/marvel) | Fleet orchestration: declarative team manifests with a reconciliation loop, k8s-style desired state pointed at agent sessions instead of containers. Heartbeats, restart policies, shift rotation for context exhaustion, tmux runtime adapters. | usable, single-host |
| [kos](https://github.com/ArcavenAE/kos) | Knowledge capture: a graph of decisions with confidence tiers (bedrock, frontier, graveyard). What was ruled out and why is first-class. Charters render from the graph, so prose cannot silently drift from the record. | usable |
| [flyloft](https://github.com/ArcavenAE/flyloft) | Knowledge retrieval: curated hybrid retrieval over the record. Sources stay verbatim; summaries are authored and marked, never auto-extracted. | early design |
| [switchboard](https://github.com/ArcavenAE/switchboard) | Remote session access: observe, inject, and debug any tmux session across hosts and NAT. SSH end-to-end, verified frames; the relay routes sessions it cannot read. | protocol proven, rebuild in progress |
| [sideshow](https://github.com/ArcavenAE/sideshow) | Configuration distribution: content packs (skills, commands, rules, hooks) with real provenance. Upstream installers run once in auditable CI; the output ships as a cosign-signed tarball with a transparency-log entry. | usable, narrow |
| [critic](https://github.com/ArcavenAE/critic) | Evaluation: a registry of agent-generated run repositories with lineage, and an arena for comparing variants. Cost is accounted per selected outcome, so discards register as screening, not waste. | designed |
| [beadle](https://github.com/ArcavenAE/beadle) | Issue triage: scores issues and PRs against a repository's declared intent, weighted by what maintainers actually act on. | running today |
| usher | Front of house: onboarding and install help for an AI tooling fleet, plus configuration and usage reporting. | design phase, private |

Two more worth knowing about:

- [callbook](https://github.com/ArcavenAE/callbook) is our work-tracking
  kit for distributed agent and human teams: an opinionated companion to
  [beads](https://github.com/gastownhall/beads), the Dolt-backed issue
  tracker we run daily and contribute to upstream.
- bmad-extras is a casting pool of domain-expert agents for BMAD-method
  workflows (private while its learning content is curated).

## How they fit together

sideshow installs the configuration. marvel declares the team and
launches it into tmux. switchboard reaches any session on any host.
Work is tracked in beads through callbook. What a session learns lands
in kos; flyloft retrieves it for the next one. critic measures what the
teams produce, beadle keeps the issue queues honest, and usher gets
people and machines set up in the first place.

The rule that holds it together: no component conscripts another. marvel
orchestrates any console, switchboard relays any tmux session, sideshow
installs into any repo, kos runs in any project. Adopt one tool, three,
or all of them, and replace any of them.

## The spirit

- **User sovereignty.** No phone-home, no lock-in, no hidden
  dependencies. You choose your agent console; the tools coordinate, they
  do not conscript.
- **Knowledge that refuses to auto-summarize.** Sources and findings
  stay verbatim; summaries are authored; the graveyard records what was
  ruled out and why. Lossy memory shipped as a default is still lossy.
- **Automation checks and proposes; humans judge.** Promotion, meaning,
  dissent, and closure remain human acts. Every automated proposal is
  confirm-or-override.
- **Gradual elaboration.** Build what you need, not what you might need.
  Prototypes graduate; they are not corrected.

*The names come from stagecraft: the atelier's dark stage, the fly
loft, the callbook, the sideshow. The register is naming, not
architecture.*
