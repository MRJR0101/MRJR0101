# GitHub Profile Improvement Plan -- MRJR0101

**Date:** 2026-03-01
**Target:** https://github.com/MRJR0101
**Executor:** Desktop Claude (via Desktop Commander MCP)
**Owner:** MR (mike_)

---

## Current State

- GitHub username: MRJR0101
- 2 public repos: CodeGraphX (substantial) and BlueWhale (empty shell)
- Profile has NO name, NO bio, NO location, NO profile picture, NO website URL
- Profile README may or may not be deployed (was created previously but push status unknown)
- GitHub Pages site at mrjr0101.github.io is NOT live
- 8 additional projects staged in C:\Repository\ but not yet pushed
- Profile is completely invisible to web search (zero results for "MRJR0101")

---

## Execution Order

Complete each phase in order. Present plan to MR and wait for approval before executing. Use Desktop Commander for ALL file operations. PowerShell 7+ only. Plain UTF-8 encoding only -- no Unicode symbols or non-ASCII characters in code or output.

---

## PHASE 1: Profile README (highest visibility impact)

### Goal
Create or update the MRJR0101/MRJR0101 repo with a profile README that renders on the GitHub profile page.

### Step 1.1: Check if repo exists
```powershell
# Check if the profile repo exists locally
Test-Path "C:\Repository\MRJR0101"

# Check if it exists on GitHub
gh repo view MRJR0101/MRJR0101 2>&1
```

### Step 1.2: Create repo if it does not exist
```powershell
# Create the special profile repo
mkdir "C:\Repository\MRJR0101"
Set-Location "C:\Repository\MRJR0101"
git init
```

### Step 1.3: Write README.md
Write exactly this content to `C:\Repository\MRJR0101\README.md`:

```markdown
# MR

Python developer building tools for observability, code intelligence, security analysis, and data pipelines.

## What I Build

**Runtime Observability**
[Eye-Witness](https://github.com/MRJR0101/Eye-Witness) -- Unified structured logging (structlog), error tracking (Sentry SDK), and distributed tracing (OpenTelemetry) for Python CLI applications. Local-first, vendor-neutral.

**Static Code Intelligence**
[CodeGraphX](https://github.com/MRJR0101/CodeGraphX) -- Tree-sitter powered code analysis pipeline with 14 CLI commands. Scan, parse, extract, query, search, compare, and analyze codebases. Uses Neo4j for graph storage.

**Security Tooling**
[BinaryGuard](https://github.com/MRJR0101/BinaryGuard) -- Binary and file security analysis toolkit.
[DreamExtractor](https://github.com/MRJR0101/DreamExtractor) -- Data extraction and domain analysis.

**Data Pipelines**
[pipeline_suite](https://github.com/MRJR0101/pipeline_suite) -- Orchestrated data processing pipelines with feed handling, encoding safety, and reporting.
[unified_url_toolkit](https://github.com/MRJR0101/unified_url_toolkit) -- URL extraction, normalization, validation, and trait enrichment.

**System Tools**
[SystemAuditor](https://github.com/MRJR0101/SystemAuditor) -- System auditing and environment analysis.
[ProjectCatalog](https://github.com/MRJR0101/ProjectCatalog) -- Project inventory and metadata cataloging.

## Stack

Python | PowerShell | structlog | OpenTelemetry | Sentry SDK | tree-sitter | Neo4j | aiohttp | typer | rich | pydantic

## Contact

Houston, TX
```

### Step 1.4: Push profile repo
```powershell
Set-Location "C:\Repository\MRJR0101"
git add README.md
git commit -m "Add profile README"

# If repo does not exist on GitHub yet:
gh repo create MRJR0101/MRJR0101 --public --source . --push

# If repo already exists:
git remote add origin https://github.com/MRJR0101/MRJR0101.git
git branch -M main
git push -u origin main
```

### Verification
- Visit https://github.com/MRJR0101 -- the README should render on the profile page
- If it does not render, confirm the repo name matches the username exactly (case-sensitive)

---

## PHASE 2: GitHub Profile Settings (manual -- MR must do this)

### Step 2.1: Set profile metadata
MR must go to https://github.com/settings/profile and set:

| Field | Value |
|-------|-------|
| Name | MR |
| Bio | Python developer. Observability, code intelligence, security tooling, data pipelines. |
| Location | Houston, TX |
| Website | https://mrjr0101.github.io (set this AFTER Phase 5 is complete) |

### Step 2.2: Pin repositories
MR must go to https://github.com/MRJR0101 and click "Customize your pins". Select these repos in this order:

1. CodeGraphX
2. Eye-Witness
3. BinaryGuard
4. DreamExtractor
5. pipeline_suite
6. unified_url_toolkit

(GitHub allows up to 6 pinned repos)

### Step 2.3: Set profile picture
MR should upload a profile picture or avatar. Even a simple initial/geometric avatar is better than the default silhouette.

---

## PHASE 3: Repository Topics (discoverability)

### Goal
Add GitHub topics to each repo so they appear in GitHub Explore and search.

### Step 3.1: Add topics via gh CLI

```powershell
# CodeGraphX
gh repo edit MRJR0101/CodeGraphX --add-topic "python,tree-sitter,code-analysis,cli,neo4j,static-analysis,code-intelligence,ast,typer"

# Eye-Witness (after push)
gh repo edit MRJR0101/Eye-Witness --add-topic "python,observability,structlog,opentelemetry,sentry,logging,tracing,json-logging,cli"

# BinaryGuard (after push)
gh repo edit MRJR0101/BinaryGuard --add-topic "python,security,binary-analysis,file-analysis,scanning"

# DreamExtractor (after push)
gh repo edit MRJR0101/DreamExtractor --add-topic "python,data-extraction,domain-analysis,scraping"

# pipeline_suite (after push)
gh repo edit MRJR0101/pipeline_suite --add-topic "python,data-pipeline,orchestration,etl,feed-processing"

# unified_url_toolkit (after push)
gh repo edit MRJR0101/unified_url_toolkit --add-topic "python,url,normalization,validation,dns,whois,tls"

# SystemAuditor (after push)
gh repo edit MRJR0101/SystemAuditor --add-topic "python,system-audit,environment,cli"

# ProjectCatalog (after push)
gh repo edit MRJR0101/ProjectCatalog --add-topic "python,project-management,catalog,metadata,cli"
```

NOTE: Topics can only be added after a repo exists on GitHub. Run the topic commands for repos that are already pushed. Queue the rest for after Phase 4.

---

## PHASE 4: Push Staged Repositories

### Prerequisites
- Deploy-ToGitHub.ps1 v3.0 must have been run successfully (copies from C:\Dev\PROJECTS\ to C:\Repository\)
- DEPLOY_REPORT.md in C:\Repository\ must show zero CRITICAL findings
- All repos are PRIVATE by default -- MR decides which to make public

### Step 4.1: Verify staging area is clean
```powershell
Set-Location "C:\Repository"
Get-Content "DEPLOY_REPORT.md" | Select-String "CRITICAL"
```
If any CRITICAL findings exist, STOP. Do not push. Fix findings first.

### Step 4.2: Push each repo
For each repo that has NOT been pushed yet, run:

```powershell
$repos = @(
    'DreamExtractor', 'BinaryGuard', 'pipeline_suite',
    'unified_url_toolkit', 'SystemAuditor', 'ProjectCatalog', 'Eye-Witness'
)

foreach ($r in $repos) {
    $repoPath = Join-Path "C:\Repository" $r
    if (-not (Test-Path $repoPath)) {
        Write-Host "SKIP: $r not found in C:\Repository" -ForegroundColor Yellow
        continue
    }

    Push-Location $repoPath

    # Initialize git if needed
    if (-not (Test-Path ".git")) {
        git init
    }

    # Install pre-commit hook
    $hookSrc = Join-Path $repoPath "hooks\pre-commit"
    $hookDst = Join-Path $repoPath ".git\hooks\pre-commit"
    if (Test-Path $hookSrc) {
        Copy-Item $hookSrc $hookDst -Force
    }

    git add .
    git commit -m "Initial commit"

    # Create as PRIVATE repo
    gh repo create "MRJR0101/$r" --private --source . --push

    Pop-Location
    Write-Host "$r pushed (PRIVATE)" -ForegroundColor Green
}
```

### Step 4.3: Make selected repos public
MR must decide which repos to make public. For each repo MR approves:

```powershell
# Example: make Eye-Witness public
gh repo edit MRJR0101/Eye-Witness --visibility public

# Repeat for each repo MR approves
```

### Step 4.4: Add topics to newly pushed repos
Re-run the topic commands from Phase 3 for any repos that were just pushed.

### Step 4.5: Handle BlueWhale
The BlueWhale repo is empty on GitHub. Two options:

Option A (recommended): Make it private until code is ready
```powershell
gh repo edit MRJR0101/BlueWhale --visibility private
```

Option B: Delete and recreate later
```powershell
gh repo delete MRJR0101/BlueWhale --yes
```

MR must choose. An empty public repo hurts more than no repo.

---

## PHASE 5: GitHub Pages Site

### Goal
Deploy a simple developer landing page at https://mrjr0101.github.io/

### Step 5.1: Create the Pages repo
```powershell
mkdir "C:\Repository\mrjr0101.github.io"
Set-Location "C:\Repository\mrjr0101.github.io"
git init
```

### Step 5.2: Write index.html
Write this file to `C:\Repository\mrjr0101.github.io\index.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MR - Python Developer</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: #0d1117;
            color: #c9d1d9;
            line-height: 1.6;
            padding: 2rem;
            max-width: 800px;
            margin: 0 auto;
        }
        h1 { color: #f0f6fc; margin-bottom: 0.5rem; font-size: 2rem; }
        h2 { color: #8b949e; font-size: 1rem; font-weight: 400; margin-bottom: 2rem; }
        h3 { color: #58a6ff; font-size: 1.1rem; margin: 2rem 0 1rem 0; }
        a { color: #58a6ff; text-decoration: none; }
        a:hover { text-decoration: underline; }
        .project {
            background: #161b22;
            border: 1px solid #30363d;
            border-radius: 6px;
            padding: 1rem 1.25rem;
            margin-bottom: 0.75rem;
        }
        .project-name { font-weight: 600; color: #58a6ff; }
        .project-desc { color: #8b949e; font-size: 0.9rem; margin-top: 0.25rem; }
        .tech {
            display: inline-block;
            background: #1f2937;
            border: 1px solid #30363d;
            border-radius: 12px;
            padding: 0.15rem 0.6rem;
            font-size: 0.8rem;
            color: #8b949e;
            margin: 0.2rem 0.2rem 0.2rem 0;
        }
        .links { margin-top: 2rem; }
        .links a {
            display: inline-block;
            margin-right: 1.5rem;
            font-size: 0.95rem;
        }
        .section { margin-bottom: 1rem; }
        footer {
            margin-top: 3rem;
            padding-top: 1.5rem;
            border-top: 1px solid #30363d;
            color: #484f58;
            font-size: 0.85rem;
        }
    </style>
</head>
<body>
    <h1>MR</h1>
    <h2>Python Developer -- Houston, TX</h2>

    <div class="section">
        <p>I build tools for observability, code intelligence, security analysis, and data pipelines. Everything is Python-first, local-first, and designed to work without vendor lock-in.</p>
    </div>

    <h3>Projects</h3>

    <div class="project">
        <a class="project-name" href="https://github.com/MRJR0101/CodeGraphX">CodeGraphX</a>
        <div class="project-desc">Tree-sitter code intelligence pipeline. 14 CLI commands for scanning, parsing, querying, and analyzing codebases. Neo4j graph storage.</div>
    </div>

    <div class="project">
        <a class="project-name" href="https://github.com/MRJR0101/Eye-Witness">Eye-Witness</a>
        <div class="project-desc">Unified observability library. Structured logging (structlog), error tracking (Sentry SDK), distributed tracing (OpenTelemetry). Local-first, vendor-neutral.</div>
    </div>

    <div class="project">
        <a class="project-name" href="https://github.com/MRJR0101/BinaryGuard">BinaryGuard</a>
        <div class="project-desc">Binary and file security analysis toolkit.</div>
    </div>

    <div class="project">
        <a class="project-name" href="https://github.com/MRJR0101/DreamExtractor">DreamExtractor</a>
        <div class="project-desc">Data extraction and domain analysis.</div>
    </div>

    <div class="project">
        <a class="project-name" href="https://github.com/MRJR0101/pipeline_suite">pipeline_suite</a>
        <div class="project-desc">Orchestrated data pipelines with feed handling, encoding safety, and reporting.</div>
    </div>

    <div class="project">
        <a class="project-name" href="https://github.com/MRJR0101/unified_url_toolkit">unified_url_toolkit</a>
        <div class="project-desc">URL extraction, normalization, validation, and trait enrichment.</div>
    </div>

    <h3>Stack</h3>
    <div class="section">
        <span class="tech">Python</span>
        <span class="tech">PowerShell</span>
        <span class="tech">structlog</span>
        <span class="tech">OpenTelemetry</span>
        <span class="tech">Sentry SDK</span>
        <span class="tech">tree-sitter</span>
        <span class="tech">Neo4j</span>
        <span class="tech">aiohttp</span>
        <span class="tech">typer</span>
        <span class="tech">rich</span>
        <span class="tech">pydantic</span>
    </div>

    <div class="links">
        <a href="https://github.com/MRJR0101">GitHub</a>
    </div>

    <footer>
        Built with plain HTML and CSS. No frameworks, no JavaScript, no tracking.
    </footer>
</body>
</html>
```

### Step 5.3: Push the Pages repo
```powershell
Set-Location "C:\Repository\mrjr0101.github.io"
git add index.html
git commit -m "Initial GitHub Pages site"
gh repo create MRJR0101/mrjr0101.github.io --public --source . --push
```

### Step 5.4: Enable GitHub Pages
MR must go to https://github.com/MRJR0101/mrjr0101.github.io/settings/pages and set:

| Setting | Value |
|---------|-------|
| Source | Deploy from a branch |
| Branch | main |
| Folder | / (root) |

Click Save. Site will be live at https://mrjr0101.github.io/ within 1-2 minutes.

### Step 5.5: Update profile website URL
After the site is live, MR must go to https://github.com/settings/profile and set:

| Field | Value |
|-------|-------|
| Website | https://mrjr0101.github.io |

---

## PHASE 6: Repository README Quality (ongoing)

### Goal
Ensure every public repo has a README that scores well.

### Minimum README checklist per repo
- [ ] Project name and one-line description
- [ ] What problem it solves (2-3 sentences)
- [ ] Quick start / installation
- [ ] Usage examples (at least one)
- [ ] Project structure (if multi-module)
- [ ] Requirements / dependencies
- [ ] License

### Repos that already have good READMEs (from previous sessions)
- CodeGraphX -- expanded README created 2026-02-28
- Eye-Witness -- README created 2026-02-28

### Repos that need README work
- BinaryGuard -- unknown state
- DreamExtractor -- unknown state
- pipeline_suite -- unknown state
- unified_url_toolkit -- unknown state
- SystemAuditor -- unknown state
- ProjectCatalog -- unknown state

For each repo, Desktop Claude should:
1. Read the current README at C:\Repository\{repo}\README.md
2. Read the source code to understand what the project does
3. Write a README following the checklist above
4. Commit and push

---

## Execution Summary

| Phase | What | Who | Blocking? |
|-------|------|-----|-----------|
| 1 | Profile README repo | Desktop Claude | No |
| 2 | Profile settings (name, bio, location, pins, avatar) | MR (manual) | No |
| 3 | Repository topics | Desktop Claude | Needs repos on GitHub |
| 4 | Push staged repos | Desktop Claude | Needs clean DEPLOY_REPORT |
| 5 | GitHub Pages site | Desktop Claude + MR (settings) | No |
| 6 | README quality pass | Desktop Claude | Needs repos on GitHub |

### Critical rules for Desktop Claude
- Use Desktop Commander for ALL file operations
- PowerShell 7+ only
- Plain UTF-8 encoding only (utf8NoBOM)
- NEVER delete files without explicit permission from MR
- Present plan and wait for approval before executing multi-step work
- Read the environment-policy skill before any file/process task
- ALL repos are PRIVATE by default -- MR explicitly decides which become public

---

## Post-Completion Verification

After all phases are complete, verify:

1. https://github.com/MRJR0101 shows profile README with project list
2. Profile has name, bio, location filled in
3. 6 repos are pinned
4. All public repos have topics set
5. https://mrjr0101.github.io/ loads and shows project list
6. BlueWhale is either private or deleted
7. Search Google for "MRJR0101 github" -- profile should start appearing within 1-2 weeks
