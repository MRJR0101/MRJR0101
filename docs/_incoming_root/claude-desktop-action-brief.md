# Claude Desktop Action Brief
# Source: Claude.ai session 2026-03-01
# Priority: Execute in order. Each section has exact commands.

---

## CONTEXT

This session audited MR's GitHub profile (MRJR0101) and all repos using the
GitHub REST API. Produced ready-to-deploy files for profile README, CodeGraphX
README, and an AI-inline learning playbook. Everything below is verified against
live API data.

MR has GitHub CLI (gh) installed. Use `gh` commands via Desktop Commander for
all GitHub operations. If auth is needed: `gh auth login` (opens browser).

---

## ENVIRONMENT RULES (always apply)

- Windows 11 Pro, username mike_, PowerShell 7.5.4 or Python only
- Desktop Commander for all file/process operations
- UTF-8 encoding only, no Unicode symbols or non-ASCII in code/output
- Never delete files without explicit permission
- Present plan and wait for approval before multi-step work
- All projects live under C:\Dev\PROJECTS\

---

## ACTION 1: Deploy CodeGraphX README (HIGHEST PRIORITY)

The current README is 1,251 bytes for a 100KB project. A new README has been
written and is ready to deploy. It includes CI badge, architecture diagram,
all 14 commands, example workflows, and security section.

### Files to deploy:

Source file (ask MR to upload or copy from claude.ai downloads):
  codegraphx-README.md -> C:\Dev\PROJECTS\CodeGraphX\README.md

### If MR uploads the file, deploy with:

```powershell
Copy-Item "PATH_TO_DOWNLOADED\codegraphx-README.md" "C:\Dev\PROJECTS\CodeGraphX\README.md" -Force
```

### Then commit and push:

```powershell
cd C:\Dev\PROJECTS\CodeGraphX
git add README.md
git commit -m "docs: expand README with architecture, commands, examples, badges"
git push origin master
```

### Verify badges render:

After push, check that these URLs resolve:
- CI badge: https://github.com/MRJR0101/CodeGraphX/actions/workflows/ci.yml/badge.svg
- The CI workflow ID is 233725664, workflow file is .github/workflows/ci.yml

---

## ACTION 2: Clean Up CodeGraphX Repo

### Remove dead files:

```powershell
cd C:\Dev\PROJECTS\CodeGraphX
git rm requirements.txt.old
git rm scripts/pre-commit.backup_20260210_150925.py
git commit -m "chore: remove dead files (requirements.txt.old, pre-commit backup)"
git push origin master
```

### Fix FEATURE_REPORT.md version header:

The file says "Version: 0.1.0" but the project is at 0.2.0. Fix the header:

```powershell
cd C:\Dev\PROJECTS\CodeGraphX
# Find and replace "Version:** 0.1.0" with "Version:** 0.2.0" in FEATURE_REPORT.md
(Get-Content FEATURE_REPORT.md) -replace '0\.1\.0', '0.2.0' | Set-Content FEATURE_REPORT.md
git add FEATURE_REPORT.md
git commit -m "docs: update FEATURE_REPORT version to 0.2.0"
git push origin master
```

### Add GitHub topics:

```powershell
gh repo edit MRJR0101/CodeGraphX --add-topic python,code-analysis,tree-sitter,neo4j,cli,static-analysis,developer-tools
```

### Create a proper GitHub Release from existing v0.2.0 tag:

There's a tag but no Release. Create one:

```powershell
gh release create v0.2.0 --repo MRJR0101/CodeGraphX --title "v0.2.0" --notes "## What's New in 0.2.0

- Incremental extract caching with metadata output
- Incremental Neo4j load with persisted load state and metrics
- Snapshot timeline workflow (snapshots list/create/diff/report)
- Delta command for snapshot-to-snapshot change summaries
- Impact command with transitive caller traversal
- Hardened Cypher execution with query parameterization
- No-DB snapshot hashing fallback from events.jsonl
- Non-DB end-to-end smoke automation (scripts/smoke_no_db.ps1)
- CI no-DB smoke job"
```

---

## ACTION 3: Create GitHub Profile README

A profile README has been written. It needs a new repo MRJR0101/MRJR0101.

### Create the repo and push:

```powershell
# Create the profile README repo
gh repo create MRJR0101 --public --description "Profile README"

# Clone it
cd C:\Dev\PROJECTS
gh repo clone MRJR0101/MRJR0101
cd MRJR0101

# Copy the README (MR will upload from claude.ai downloads)
Copy-Item "PATH_TO_DOWNLOADED\github-profile-README.md" "C:\Dev\PROJECTS\MRJR0101\README.md" -Force

# Commit and push
git add README.md
git commit -m "docs: add profile README"
git push origin main
```

### Verify:

Visit https://github.com/MRJR0101 -- the README should render on the profile page.

---

## ACTION 4: Set GitHub Profile Basics

```powershell
# These must be set via GitHub web UI (Settings -> Profile)
# Direct MR to: https://github.com/settings/profile
```

Fields to set:
- Name: [MR's preferred display name -- ask them]
- Bio: "Building Python tools for code intelligence, observability, and AI orchestration."
- Location: [ask MR if they want to share]

---

## ACTION 5: Handle BlueWhale

The BlueWhale repo is COMPLETELY EMPTY on GitHub. Created 2026-01-29, nothing
pushed. Description has a typo ("informaton" -> "information").

### Check if local code exists:

```powershell
# Check if there's a BlueWhale directory with code
Test-Path "C:\Dev\PROJECTS\BlueWhale"
if (Test-Path "C:\Dev\PROJECTS\BlueWhale") {
    Get-ChildItem "C:\Dev\PROJECTS\BlueWhale" -Recurse | Measure-Object
    Get-ChildItem "C:\Dev\PROJECTS\BlueWhale" -Depth 2
}
```

### Decision tree:

IF local code exists:
  -> Push it to GitHub with proper README, LICENSE, .gitignore

IF no local code:
  -> ASK MR: "BlueWhale is empty on GitHub and I don't see local code.
     Should we make it private until it has content, or keep it public?"
  -> If making private: `gh repo edit MRJR0101/BlueWhale --visibility private`

### Fix the typo regardless:

```powershell
gh repo edit MRJR0101/BlueWhale --description "Interwoven Systems Involving 4 AIs in concert gathering information and automatically uploading into Database and PersonalLibrary"
```

---

## ACTION 6: Push Eye-Witness to GitHub

Eye-Witness is complete at C:\Dev\PROJECTS\Eye-Witness but not on GitHub yet.

### Verify local state first:

```powershell
cd C:\Dev\PROJECTS\Eye-Witness
Test-Path pyproject.toml
Test-Path src\eye_witness\__init__.py
Test-Path tests\test_eye_witness.py
Test-Path README.md
Test-Path LICENSE
Test-Path .gitignore
```

### Create repo and push:

```powershell
gh repo create Eye-Witness --public --description "Python observability library unifying structlog, Sentry SDK, and OpenTelemetry. Local-first, vendor-neutral, zero-config." --license mit

cd C:\Dev\PROJECTS\Eye-Witness
git remote add origin https://github.com/MRJR0101/Eye-Witness.git
git branch -M main
git push -u origin main
```

### Add topics:

```powershell
gh repo edit MRJR0101/Eye-Witness --add-topic python,observability,structlog,opentelemetry,sentry,logging,tracing,monitoring
```

### Quality checks before push:

If README.md is missing or minimal, create one. The Eye-Witness README should
cover:
- What it does (unifies structlog + Sentry + OpenTelemetry)
- Quick start (from eye_witness import init; init(service_name="my-app"))
- Three-path architecture explanation
- Local-first design philosophy
- Installation: uv pip install -e ".[all]"

If LICENSE is missing, create MIT license.
If .gitignore is missing, create standard Python .gitignore.

---

## ACTION 7: Star Dependencies and Follow Accounts

```powershell
# Star the tools MR depends on
gh api -X PUT user/starred/hynek/structlog
gh api -X PUT user/starred/getsentry/sentry-python
gh api -X PUT user/starred/open-telemetry/opentelemetry-python
gh api -X PUT user/starred/fastapi/typer
gh api -X PUT user/starred/Textualize/rich
gh api -X PUT user/starred/tree-sitter/tree-sitter
gh api -X PUT user/starred/tree-sitter/py-tree-sitter
gh api -X PUT user/starred/neo4j/neo4j-python-driver
gh api -X PUT user/starred/astral-sh/uv
gh api -X PUT user/starred/astral-sh/ruff
gh api -X PUT user/starred/samuelcolvin/pydantic

# Follow relevant accounts/orgs
gh api -X PUT user/following/hynek
gh api -X PUT user/following/open-telemetry
gh api -X PUT user/following/getsentry
gh api -X PUT user/following/astral-sh
```

---

## ACTION 8: Pin Repos on Profile

This must be done via GitHub web UI:
https://github.com/MRJR0101 -> "Customize your pins"

Pin order (most impressive first):
1. CodeGraphX
2. Eye-Witness (after it's pushed)
3. BlueWhale (only if it has content)

---

## SUPPLEMENTARY FILES PRODUCED THIS SESSION

All available in MR's claude.ai downloads:

1. **claude-desktop-handoff-v2.md**
   Full ecosystem handoff with all project details, file trees, quality audit
   findings. This is the master reference document.

2. **ai-inline-learning-playbook.md**
   Practical guide for AI continuity across conversations. Contains patterns,
   code examples, anti-patterns, and the multi-agent event logging system.
   Recommended location: C:\Dev\PROJECTS\_PRIME\playbooks\

3. **github-profile-README.md**
   Ready to deploy as C:\Dev\PROJECTS\MRJR0101\README.md

4. **codegraphx-README.md**
   Ready to deploy as C:\Dev\PROJECTS\CodeGraphX\README.md

5. **github-private-access-guide.md**
   Three methods for giving Claude access to private repos.
   Recommended: Use `gh` CLI since MR already has it installed.
   Recommended location: C:\Dev\PROJECTS\_PRIME\guides\

6. **eye-witness-handoff.md**
   Deep Eye-Witness-specific context document from earlier in the session.

---

## KEY INSIGHTS FROM GITHUB AUDIT

### CodeGraphX is strong but undersold
- 100KB of real Python code with CI, tests, docs, security architecture
- 14 CLI commands covering scan -> parse -> extract -> load -> analyze pipeline
- CI matrix: ubuntu + windows, Python 3.10-3.13, both passing
- Has v0.2.0 tag but no GitHub Release (missed visibility)
- README was 1.2KB for a serious project -- fixed in new README

### BlueWhale is hurting the profile
- Empty repo with a typo signals incomplete follow-through
- Either push code or make private -- empty public repos are worse than no repo

### Profile is invisible
- No name, bio, location, profile README
- Zero stars, zero following, zero followers
- Account is 10 months old with 1 visible public event
- All fixable in 30 minutes

### Eye-Witness is the hidden gem
- Complete, tested, not on GitHub at all
- Would immediately become the second strongest repo

### The ecosystem story is compelling
- Runtime observability + static code intelligence + AI orchestration
- Each project has clear boundaries and integration points
- The profile README frames this narrative

---

## VERIFICATION CHECKLIST (Run After All Actions)

```powershell
# Check all repos exist and have content
gh repo list MRJR0101 --limit 10

# Check topics are set
gh api repos/MRJR0101/CodeGraphX --jq '.topics'
gh api repos/MRJR0101/Eye-Witness --jq '.topics'

# Check releases exist
gh release list --repo MRJR0101/CodeGraphX

# Check profile README renders
gh api repos/MRJR0101/MRJR0101/contents/README.md --jq '.size'

# Check BlueWhale description fixed
gh api repos/MRJR0101/BlueWhale --jq '.description'

# Check starred repos
gh api user/starred --jq '.[].full_name' | Select-Object -First 15
```

---

## WHAT NOT TO DO

- Do not expand Eye-Witness scope beyond 7 core modules
- Do not delete any files without MR's explicit permission
- Do not push without MR reviewing the changes first
- Do not use Unicode symbols in any code or output
- Do not commit tokens, credentials, or .env files
- Do not change CodeGraphX default branch from master (MR's choice)
- Present plan and wait for approval before executing
