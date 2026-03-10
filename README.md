<h1 align="center">
  MR &middot; MRJR0101
</h1>h1>

<h4 align="center">Security tooling. Code intelligence. Zero-dependency Python. Built to last.</h4>h4>

<p align="center">
  <a href="https://github.com/MRJR0101?tab=repositories"><img src="https://img.shields.io/badge/projects-60%2B-blue?style=flat-square"></a>a>
    <a href="https://github.com/MRJR0101/MRJR0101#tech-stack"><img src="https://img.shields.io/badge/language-Python-yellow?style=flat-square"></a>a>
      <a href="https://www.linkedin.com/in/michael-rawls-jr"><img src="https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=flat-square&logo=linkedin"></a>a>
        <a href="https://mrjr0101.github.io"><img src="https://img.shields.io/badge/Portfolio-Visit-green?style=flat-square"></a>a>
          <img src="https://img.shields.io/badge/CompTIA-A%2B%20%7C%20Network%2B-red?style=flat-square">
</p>p>

<p align="center">
  <a href="#what-im-building">Projects</a>a> &bull;
    <a href="#security-tooling">Security</a>a> &bull;
      <a href="#tech-stack">Stack</a>a> &bull;
        <a href="#design-philosophy">Philosophy</a>a> &bull;
          <a href="#background">Background</a>a>
</p>p>

---

Python developer with 24 years of technical experience building tools that solve real problems. I write local-first, zero-dependency automation -- CLI tools, security scanners, observability libraries, and code intelligence pipelines. I've built 60+ production projects spanning web scraping, database management, file operations, security tooling, and AI agent orchestration. Everything I ship works offline, runs on a single machine, and does exactly what it says.

---

## What I'm Building

### Code Intelligence & Observability

**[CodeGraphX](https://github.com/MRJR0101/CodeGraphX)** -- Deterministic code intelligence pipeline. Scans repositories with tree-sitter, extracts semantic facts (functions, calls, imports), builds a knowledge graph, and runs impact analysis, duplicate detection, and snapshot diffs. 14 CLI commands covering the full lifecycle from scan to query. CI-tested across Python 3.10-3.13 on Ubuntu and Windows.

**[Eye-Witness](https://github.com/MRJR0101/Eye-Witness)** -- Python observability library that unifies structured logging (structlog), error tracking (Sentry SDK), and distributed tracing (OpenTelemetry) into one package. Every log line carries trace context automatically. No DSN required -- works locally with zero config.

---

## Security Tooling

I build security tools aligned with the same philosophy behind the [ProjectDiscovery](https://projectdiscovery.io) ecosystem -- fast, focused, open, and built for real-world attack surfaces.

**PyToolbelt** *(publishing ongoing)* -- a collection of 60+ single-file Python tools across 25 categories:

| Category | Tools |
|---|---|
| **Security** | PE scanners, quarantine management, binary verification |
| **Networking** | Port scanners, DNS tools, certificate checkers |
| **Scraping** | Multi-plugin scrapers, SEO indexers, link analysis |
| **FileOps** | Inventory tools, tree builders, duplicate finders |
| **Database** | SQLite/PostgreSQL utilities, migration tools, schema managers |
| **Archive** | Compression utilities, backup automation |
| **Meta** | Project indexers, content search, catalog generators |

Each tool: zero external dependencies &middot; argparse CLI &middot; unittest coverage &middot; `VERIFY.md` proving it works.

**[BinaryGuard](https://github.com/MRJR0101)** *(in development)* -- PE scanner and quarantine ecosystem for Windows. Detects, isolates, and tracks suspicious binaries on local systems.

**[unified_url_toolkit](https://github.com/MRJR0101/unified_url_toolkit)** -- URL extraction, normalization, and analysis pipeline with DNS, WHOIS, and TLS lookups. Built for large-scale domain intelligence and recon workflows.

---

## AI & Learning Infrastructure

**[AI-Inline-Learning](https://github.com/MRJR0101/AI-Inline-Learning)** -- A methodology for embedding guidance directly in code comments so AI agents build collective intelligence across sessions. Instead of losing context between conversations, the codebase itself becomes the knowledge transfer mechanism. Validated against 30+ academic papers with measurable error reduction.

---

## Tech Stack

```
Languages     Python · PowerShell · SQL
Analysis      tree-sitter · Neo4j · JSONL pipelines
Observability structlog · OpenTelemetry · Sentry SDK
Tooling       uv · argparse · unittest · SQLite
Platforms     Windows 11 · Ubuntu (CI)
Certs         CompTIA A+ · CompTIA Network+
Education     Cybersecurity -- Alvin Community College
```

---

## Design Philosophy

- **Zero dependencies** -- if stdlib can do it, no pip install needed
- - **Single-file tools** -- one script, one job, easy to audit
  - - **Local-first** -- everything works offline, no cloud required
    - - **Deterministic** -- same input, same output, every time
      - - **Resume-capable** -- long operations pick up where they left off
       
        - ---

        ## Background

        I didn't start in software. I spent years managing restaurant operations, running commercial electrical installations for Fortune 500 clients, and building solar arrays. That operational background shows up in how I write code -- systematic, documented, built to survive real-world conditions. I transitioned to full-time development in 2024 and haven't looked back.

        ---

        ## Current Focus

        - Publishing more PyToolbelt tools as standalone repos
        - - Expanding CodeGraphX with richer graph queries
          - - Shipping BinaryGuard -- PE scanner and quarantine ecosystem for Windows
            - - Shipping AI-Inline-Learning documentation and examples
             
              - ---

              [Portfolio](https://mrjr0101.github.io) &middot; [LinkedIn](https://www.linkedin.com/in/michael-rawls-jr) &middot; rawlsjrm@gmail.com
