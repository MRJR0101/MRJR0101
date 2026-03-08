# Hey, I'm MR

Python developer with 24 years of technical experience building tools that solve
real problems. I write local-first, zero-dependency automation -- CLI tools,
security scanners, observability libraries, and code intelligence pipelines.

I've built 60+ production projects spanning web scraping, database management,
file operations, security tooling, and AI agent orchestration. Everything I ship
works offline, runs on a single machine, and does exactly what it says.

---

## What I'm Building

### Code Intelligence & Observability

Two projects that give you full visibility into your code -- what it looks like
statically, and what it does at runtime.

**[CodeGraphX](https://github.com/MRJR0101/CodeGraphX)** --
Deterministic code intelligence pipeline. Scans repositories with tree-sitter,
extracts semantic facts (functions, calls, imports), builds a knowledge graph,
and runs impact analysis, duplicate detection, and snapshot diffs. 14 CLI
commands covering the full lifecycle from scan to query. CI-tested across
Python 3.10-3.13 on Ubuntu and Windows.

**[Eye-Witness](https://github.com/MRJR0101/Eye-Witness)** --
Python observability library that unifies structured logging (structlog), error
tracking (Sentry SDK), and distributed tracing (OpenTelemetry) into one package.
Every log line carries trace context automatically. No DSN required -- works
locally with zero config.

### The Larger Toolkit

These public repos are the tip of the iceberg. Behind the scenes I maintain
**PyToolbelt** -- a collection of 60+ single-file Python tools organized across
25 categories:

- **Security** -- PE scanners, quarantine management, binary verification
- **FileOps** -- inventory tools, tree builders, duplicate finders
- **Scraping** -- multi-plugin scrapers, SEO indexers, link analysis
- **Database** -- SQLite/PostgreSQL utilities, migration tools, schema managers
- **Networking** -- port scanners, DNS tools, certificate checkers
- **Archive** -- compression utilities, backup automation
- **Meta** -- project indexers, content search, catalog generators

Each tool follows strict standards: zero external dependencies, argparse CLI,
unittest coverage, snake_case functions, and a VERIFY.md proving it works.

More of these are coming to GitHub as I clean and publish them.

### AI Inline Learning

**[AI-Inline-Learning](https://github.com/MRJR0101/AI-Inline-Learning)** --
A methodology for embedding guidance directly in code comments so AI agents
build collective intelligence across sessions. Instead of losing context between
conversations, the codebase itself becomes the knowledge transfer mechanism.
Validated against 30+ academic papers with measurable error reduction.
The pattern is simple, effective, and works with any LLM.

### URL & SEO Tooling

**[unified_url_toolkit](https://github.com/MRJR0101/unified_url_toolkit)** --
URL extraction, normalization, and analysis pipeline with DNS, WHOIS, and TLS
lookups. Built for large-scale SEO automation and domain intelligence work.

---

## Tech Stack

```
Languages     Python, PowerShell, SQL
Analysis      tree-sitter, Neo4j, JSONL pipelines
Observability structlog, OpenTelemetry, Sentry SDK
Tooling       uv, argparse, unittest, SQLite
Platforms     Windows 11, Ubuntu (CI)
Certs         CompTIA A+, CompTIA Network+
Education     Cybersecurity (Alvin Community College)
```

---

## Design Philosophy

- **Zero dependencies** -- if stdlib can do it, no pip install needed
- **Single-file tools** -- one script, one job, easy to audit
- **Local-first** -- everything works offline, no cloud required
- **Deterministic** -- same input, same output, every time
- **Resume-capable** -- long operations pick up where they left off

---

## Background

I didn't start in software. I spent years managing restaurant operations,
running commercial electrical installations for Fortune 500 clients, and
building solar arrays. That operational background shows up in how I write
code -- systematic, documented, built to survive real-world conditions.

I transitioned to full-time development in 2024 and haven't looked back.

---

## Current Focus

- Publishing more PyToolbelt tools as standalone repos
- Expanding CodeGraphX with richer graph queries
- Building BinaryGuard -- a PE scanner and quarantine ecosystem for Windows
- Shipping AI-Inline-Learning documentation and examples

---

[Portfolio](https://mrjr0101.github.io) | [LinkedIn](https://www.linkedin.com/in/michael-rawls-jr) | rawlsjrm@gmail.com
