# Hey, I'm MR

I build Python tools for code intelligence, observability, and AI orchestration.

Everything I ship is local-first, vendor-neutral, and designed to work without
network dependencies out of the box.

---

## What I'm Building

### The Ecosystem

Three projects that work together to give you full visibility into your code --
what it looks like, what it does at runtime, and how to coordinate AI agents
around it.

**[CodeGraphX](https://github.com/MRJR0101/CodeGraphX)** --
Deterministic code intelligence pipeline. Scans repositories with tree-sitter,
extracts semantic facts (functions, calls, imports), builds a knowledge graph,
and runs impact analysis, duplicate detection, and snapshot diffs. 14 CLI
commands covering the full lifecycle from scan to query.

**Eye-Witness** *(coming soon)* --
Python observability library that unifies structured logging (structlog), error
tracking (Sentry SDK), and distributed tracing (OpenTelemetry) into a single
package. Every log line carries trace context. No DSN required -- works locally
with zero config.

**BlueWhale** *(in progress)* --
Multi-AI orchestration system. Coordinates multiple AI agents for information
gathering, analysis, and automated knowledge management.

### How They Connect

```
CodeGraphX ---- static code structure ----> Knowledge Graph
Eye-Witness --- runtime behavior ---------> Structured Logs + Traces
BlueWhale ----- AI coordination ----------> Automated Workflows
                                               |
                          All observable, all traceable, all local-first
```

---

## Tech Stack

`Python` `tree-sitter` `structlog` `OpenTelemetry` `Sentry SDK` `Neo4j`
`typer` `rich` `pydantic` `uv`

---

## Current Focus

- Polishing CodeGraphX for wider use
- Shipping Eye-Witness as a standalone package
- Designing BlueWhale's multi-agent architecture
