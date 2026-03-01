# MR Project Ecosystem - Handoff for Claude Desktop

## MISSION

Audit all projects for pro quality, ensure everything at C:\Dev\PROJECTS\ and on
the GitHub profile (https://github.com/MRJR0101) is polished, professional, and
ready for consolidation into a cohesive ecosystem.

---

## DEVELOPMENT ENVIRONMENT

- Windows 11 Pro, username mike_
- Home directory: C:\Users\mike_
- Email: rawlsjrm@gmail.com
- PowerShell 7.5.4 or Python only
- Package management via uv
- Plain UTF-8 encoding only -- no Unicode symbols or non-ASCII characters in code or output
- All file operations via Desktop Commander -- never use bash_tool or Linux container
- Never delete files without explicit permission
- Present plan and wait for approval before executing multi-step work
- GitHub: https://github.com/MRJR0101

---

## PROJECT LOCATIONS

All consolidated projects live under: C:\Dev\PROJECTS\

---

## THE ECOSYSTEM (3 Known Projects)

### 1. Eye-Witness (COMPLETE)
- Location: C:\Dev\PROJECTS\Eye-Witness\
- GitHub: https://github.com/MRJR0101 (not yet pushed as a public repo -- check)
- Role: Observability infrastructure library (dependency for all other projects)
- Status: Functionally complete, 26 passing tests, all integration demos work

What it does: Unifies structured logging (structlog), error tracking (Sentry SDK),
and distributed tracing (OpenTelemetry) into a single Python package. The critical
integration feature is a log correlation bridge that injects trace_id and span_id
from OpenTelemetry spans into structlog JSON output.

Package structure:
```
Eye-Witness\
    pyproject.toml
    src\
        eye_witness\
            __init__.py
            _config.py        # EyeWitnessConfig dataclass with from_env()
            _init.py          # Single entry point: init() wires up all three paths
            _logging.py       # 6 structlog configuration patterns
            _sentry.py        # Sentry SDK + breadcrumb management (5 categories)
            _tracing.py       # OpenTelemetry setup + Console/OTLP HTTP/gRPC exporters
            _context.py       # Log correlation bridge (trace_id/span_id injection)
    tests\
        test_eye_witness.py   # 26 passing tests
    examples\
        cli_demo.py           # Full integration demo
```

Key design decisions (MR explicitly chose these):
- Local-first: works without network dependencies
- No-DSN = Sentry disabled (no-op), no OTLP endpoint = console export only
- Scoped to exactly 7 core modules -- rejected proposals for context propagation
  helpers, CLI command decorators, and span events helpers
- Vendor neutral via OpenTelemetry (backends swappable via env vars)
- CLI-focused, not web framework focused

Has a convenience init function:
```python
from eye_witness import init
init(service_name="my-app")  # wires up all three paths with sensible defaults
```

Also has shutdown() that handles both sentry_sdk.flush() and
TracerProvider.shutdown() in one call for CLI exit handlers.

Reference documents (in the Eye-Witness Claude Project):
- path1-structlog-reference.md
- path2-sentry-sdk-reference.md
- path3-opentelemetry-reference.md

How other projects consume it:
```powershell
uv pip install -e "C:\Dev\PROJECTS\Eye-Witness[all]"
```


### 2. BlueWhale
- Location: Unknown local path (check C:\Dev\PROJECTS\ or ask MR)
- GitHub: https://github.com/MRJR0101/BlueWhale (public)
- Role: Orchestrator / AI coordination system
- Status: Unknown -- needs audit

Description from GitHub: "Interwoven Systems Involving 4 AIs in concert gathering
information and automatically uploading into Database and PersonalLibrary"

This appears to be the main orchestrator project. It coordinates multiple AI systems
working together, with automated data collection and storage into a database and
personal knowledge library. This is likely the consolidation target for MR's
~4 orchestrator-type projects.

FIRST TASK: Read the repo contents, understand the current state, assess quality.
Check for: README completeness, code structure, tests, .gitignore, LICENSE,
consistent formatting, meaningful documentation.


### 3. CodeGraphX
- Location: Unknown local path (check C:\Dev\PROJECTS\ or ask MR)
- GitHub: https://github.com/MRJR0101/CodeGraphX (public, Python)
- Role: Static code intelligence / analysis
- Status: Unknown -- needs audit

Description from GitHub: "CodeGraphX is a deterministic code intelligence pipeline
that scans source repositories, parses code into structured facts, builds a graph of
projects/files/functions/calls, and enables fast impact [analysis]"

This is a code analysis tool that builds a dependency/call graph from source code.
It would pair naturally with Eye-Witness: CodeGraphX tells you what the code
structure looks like statically, Eye-Witness tells you what happened at runtime.
Together they provide both sides of the audit picture.

FIRST TASK: Same as BlueWhale -- read repo, assess quality, identify gaps.


---

## CONSOLIDATION CONTEXT

MR has approximately 4 orchestrator-type projects that evolved separately. The goal
is to consolidate without losing capability. Key questions still open:

1. What are all 4 orchestrators and what does each do?
2. Where do they overlap?
3. Do they collapse into BlueWhale as the single orchestrator, or do some stay
   distinct?
4. How does each one consume Eye-Witness for observability?

Eye-Witness is settled as the shared observability infrastructure -- it should be a
dependency of the orchestrators, not embedded in them.

The ecosystem architecture appears to be:
- Eye-Witness = records what happens (observability layer)
- BlueWhale = coordinates what happens (orchestrator)
- CodeGraphX = understands code structure (static analysis)

Together: runtime behavior + execution coordination + static code intelligence.

---

## QUALITY AUDIT CHECKLIST (Apply to Each Project)

### Repository Quality
- [ ] README.md: Clear purpose, installation instructions, usage examples, architecture overview
- [ ] LICENSE file present and appropriate
- [ ] .gitignore properly configured for Python projects
- [ ] pyproject.toml or setup.py with proper metadata
- [ ] No sensitive data (API keys, DSNs, passwords) in committed files
- [ ] .env.example for environment variable documentation
- [ ] Consistent code formatting throughout

### Code Quality
- [ ] All source files have module docstrings
- [ ] Functions/classes have clear docstrings
- [ ] No hardcoded paths or credentials
- [ ] Proper error handling
- [ ] Type hints where appropriate
- [ ] No dead code or commented-out blocks
- [ ] Imports organized and clean
- [ ] UTF-8 encoding, no non-ASCII characters in code

### Testing
- [ ] Tests exist and pass
- [ ] Test coverage is meaningful (not just happy path)
- [ ] Tests can run independently (no external dependencies required)

### GitHub Profile Quality
- [ ] Each repo has a clear, professional description
- [ ] Topics/tags are set on each repo
- [ ] Profile README exists (MRJR0101/MRJR0101 repo) describing the ecosystem
- [ ] Repos show the relationship between projects

---

## GITHUB PROFILE ENHANCEMENT PLAN

Current state: 2 public repos (BlueWhale, CodeGraphX), no profile README.

Recommended additions:
1. Create MRJR0101/MRJR0101 repo with a profile README that describes:
   - Who MR is (brief, professional)
   - The project ecosystem and how the pieces fit together
   - Current projects and their status
2. Push Eye-Witness as a third public repo (if not already there)
3. Add topics to each repo (python, observability, code-analysis, etc.)
4. Ensure each repo has a polished README

---

## EXECUTION ORDER

1. Start by reading the current state of each project on disk at C:\Dev\PROJECTS\
2. Read each GitHub repo to compare local vs remote state
3. Audit Eye-Witness first (known complete -- verify and polish)
4. Audit CodeGraphX (Python, likely more structured)
5. Audit BlueWhale (orchestrator, likely most complex)
6. Create/update GitHub profile README
7. Push all updates to GitHub
8. Address the orchestrator consolidation question once all projects are understood

---

## WHAT NOT TO DO

- Do not delete any files without explicit permission from MR
- Do not expand Eye-Witness scope beyond the 7 core modules
- Do not add application-specific logic to Eye-Witness
- Do not assume what the orchestrators do -- read them first
- Do not use bash_tool or Linux container -- Desktop Commander only
- Do not use Unicode symbols or non-ASCII characters in any code or output
- Present plans and wait for approval before executing multi-step work
