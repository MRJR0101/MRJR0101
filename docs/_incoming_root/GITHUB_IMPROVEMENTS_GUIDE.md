# GitHub Profile Improvements Guide
# ===================================
# Generated: March 1, 2026
# For: github.com/MRJR0101

## STEP 1: Make BlueWhale Private
---------------------------------------
Go to: https://github.com/MRJR0101/BlueWhale/settings
Scroll to "Danger Zone" > "Change visibility" > "Make private"
Reason: Empty repo with 0 KB hurts credibility


## STEP 2: Replace Your Profile README
---------------------------------------
The new README.md file (included alongside this guide) replaces
the content in your MRJR0101/MRJR0101 repo.

Option A - GitHub Web Editor:
  1. Go to https://github.com/MRJR0101/MRJR0101
  2. Click README.md
  3. Click the pencil icon (Edit)
  4. Select all, delete, paste the new content
  5. Click "Commit changes"

Option B - Git CLI:
  cd to your local clone of MRJR0101/MRJR0101
  Replace README.md with the new file
  git add README.md
  git commit -m "Upgrade profile README"
  git push


## STEP 3: Fix CodeGraphX Repo Metadata
---------------------------------------
Go to: https://github.com/MRJR0101/CodeGraphX (main page)
Click the gear icon next to "About" (top right of repo page)

Update description to:
  Deterministic code intelligence pipeline. Scans repos with tree-sitter, builds knowledge graphs, runs impact analysis and snapshot diffs. 14 CLI commands. CI-tested Python 3.10-3.13.

Add these topics (if not already there):
  python, tree-sitter, code-analysis, knowledge-graph, static-analysis,
  developer-tools, cli, neo4j, jsonl, impact-analysis

Add website URL:  (leave blank for now, or add docs link later)


## STEP 4: Fix Eye-Witness Repo Metadata
---------------------------------------
Go to: https://github.com/MRJR0101/Eye-Witness (main page)
Click the gear icon next to "About"

Current description is good. Consider adding topics:
  python, observability, structlog, opentelemetry, sentry,
  logging, tracing, monitoring, developer-tools, local-first

License shows as "Other" -- if you intended MIT, check the LICENSE
file in the repo and make sure it says MIT at the top.


## STEP 5: Pin Your Best Repos
---------------------------------------
Go to: https://github.com/MRJR0101
Click "Customize your pins" (appears when you hover near pinned section)
Pin these in order:
  1. CodeGraphX      (your flagship -- biggest, most active)
  2. Eye-Witness     (clean, professional, shows observability chops)

That is all you have public right now. As you publish more repos,
pin up to 6 total. Good future candidates:
  - BinaryGuard (security scanner)
  - Any PyToolbelt standalone tool
  - AI-Inline-Learning (rebuild and republish)


## STEP 6: Profile Settings
---------------------------------------
Go to: https://github.com/settings/profile

Check these fields:
  Name:     MR  (already set)
  Bio:      Building Python tools for code intelligence, observability, and AI orchestration.  (already set, good)
  Location: Houston, TX  (already set)
  Blog:     (empty -- consider adding your LinkedIn URL for now)
            https://www.linkedin.com/in/michael-rawls-jr
  Company:  (empty -- could add "Independent" or leave blank)


## STEP 7: Follow Some People
---------------------------------------
0 followers / 0 following looks like a ghost account.
Follow 15-20 developers in your areas of interest:
  - Python tool builders
  - tree-sitter contributors
  - OpenTelemetry maintainers
  - Security tool developers
  - People whose repos you actually use

This makes your profile look active and connected.


## STEP 8: Future Repos to Publish
---------------------------------------
Priority order for maximum profile impact:

1. BinaryGuard - PE scanner + quarantine system
   Why: Security tools get attention, unique concept,
   shows Windows expertise

2. A PyToolbelt standalone tool (pick your best one)
   Why: Demonstrates your zero-dependency philosophy

3. AI-Inline-Learning (rebuild)
   Why: Original methodology, thought leadership piece,
   good for your brand

4. A scraping tool (sanitized)
   Why: Shows practical automation skills

For each new repo before publishing:
  - Remove hardcoded paths (C:\Users\mike_\...)
  - Remove API keys, tokens, credentials
  - Remove client-specific references
  - Add MIT LICENSE file
  - Add .gitignore for Python
  - Write a solid README with install/usage/examples
  - Add topics (5-10 relevant tags)
  - Add a description in repo settings


## SUMMARY OF CHANGES
---------------------------------------
[x] New profile README drafted (see README.md file)
[ ] Make BlueWhale private
[ ] Replace profile README on GitHub
[ ] Update CodeGraphX description and topics
[ ] Fix Eye-Witness license display
[ ] Pin CodeGraphX and Eye-Witness
[ ] Add LinkedIn as blog URL in profile settings
[ ] Follow 15-20 developers
[ ] Plan next repo to publish
